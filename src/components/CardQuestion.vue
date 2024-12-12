<template>
    <div class="card">
        <div class="card__header">
            <p>Текущий вопрос: {{ id }} из {{ amountQuestions }}</p>
        </div>
        <div class="card__body">
            <h2>{{ title }}</h2>
            <p>{{ descr }}</p>
        </div>
        <div class="card__footer">
            <div class="card__form">
                <label class="card__item" v-for="option in options" :key="option.id">
                    <input class="card__input"
                    :type="type" 
                    :value="option.title" 
                    :name="id" 
                    v-model="selectedOptions"> 
                    {{ option.title }}
                </label>
                <textarea class="card__textarea" v-model:="textareaResults" v-if="enableField" />
                <UIButton class="buttonPrimary" @onClick="onSubmit"/>
            </div>
        </div>
    </div>
</template>

<script>
import { computed, ref } from 'vue';
import UIButton from './UI/UIButton.vue';



export default {
    components: {
        UIButton
    },
    props: {
        title: {
            type: String,
            required: true
        },
        descr: {
            type: String,
            required: true,
        },
        options: {
            type: Array,
            required: true,
        },
        id: {
            type: Number,
            required: true,
        },
        someAnswer: {
            type: Boolean,
            default: false
        },
        enableField: {
            type: Boolean,
            default: false
        },
        amountQuestions: {
            type: Number,
            required: true
        },
    },
    setup(props, {emit}) {

        const type = computed(() => {
            return props.someAnswer ? "checkbox" : "radio";
        });
        const textareaResults = ref("");

        const selectedOptions = ref(null);

        const onSubmit = (() => {

            let result = [];
            
            if(Array.isArray(selectedOptions.value)) {
                result.push(...selectedOptions.value, textareaResults.value)
            } else {
                result.push(selectedOptions.value, textareaResults.value)
            }

            emit("onSubmit", {id: props.id, results: result})
            

            result = [];
            selectedOptions.value = [];
            textareaResults.value = "";
        });

        return {type, textareaResults, selectedOptions, onSubmit }
    }
}
</script>