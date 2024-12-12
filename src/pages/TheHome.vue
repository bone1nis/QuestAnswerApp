<template>
    <main class="body">
        <div class="wrapper">
            <section class="start" v-if="isFinishTest">
            <div class="welcome" v-if="isNotStarting">
                <h1 class="welcome__title">Для начала прохождения нажмите на кнопку ниже. Все данные берутся из questions.json, где можно настроить конфигурацию, удачи!</h1>
                <UIButton class="buttonOrange welcome__button" :title="textStartButton" @onClick="handleClickStart"/>
            </div>
                <CardQuestion 
                v-else 
                :title="currentQuestion.question.title" 
                :descr="currentQuestion.question.descr" 
                :options="currentQuestion.question.options" 
                :id="currentQuestion.question.id"
                :enableField="currentQuestion.question.enableField"
                :someAnswer="currentQuestion.question.someAnswer"
                :amountQuestions="amountQuestions"
                @onSubmit="handleSubmit"
                />
            </section>
            <section class="finish" v-else>
                <h2 class="finish__title">Спасибо за прохождение теста, вот Ваши ответы</h2>
                <div class="finish__card" v-for="(answer, index) of answers" :key="index">
                    <div class="answer">
                        <h3 class="answer__title">{{ answer.id }}:</h3>
                        <p class="answer__text" v-for="(result, index) of answer.results" :key="index">{{ result }}</p>
                    </div>
                </div>
            </section>
        </div>
    </main>
</template>

<script>
import CardQuestion from "@/components/CardQuestion.vue";
import UIButton from "@/components/UI/UIButton.vue";

import questions from "@/seeders/questions.json"

import {reactive, ref} from "vue"
export default {
    components: {
        UIButton,
        CardQuestion
    },
    setup() {
        const isNotStarting = ref(true);
        const isFinishTest = ref(true);
        const textStartButton = "Начать тест";

        const amountQuestions = questions.length;

        let answers = ref([]);

        const currentQuestion = reactive({
            question: {},
            number: 0
        });

        const changeisNotStarting = (() => isNotStarting.value = !isNotStarting.value);

        const changeFinishTest = (() => isFinishTest.value = !isFinishTest.value);

        const handleClickStart = (() => {
            currentQuestion.question = questions[0];

            changeisNotStarting();
        });

        const handleSubmit = ((result) => {
            answers.value.push(result);

            currentQuestion.number+=1

            if (questions[ currentQuestion.number ]) {
                currentQuestion.question = questions[ currentQuestion.number ];
            } else {
                changeFinishTest();

                console.log(answers.value);
            }
        });

        return {isNotStarting, isFinishTest, textStartButton, amountQuestions, currentQuestion, answers, handleClickStart, handleSubmit};
    }
}
</script>