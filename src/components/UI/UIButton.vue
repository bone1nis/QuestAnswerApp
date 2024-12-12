<template>
    <button @click="onClick">{{ title }}</button>
</template>

<script>
export default {
    props: {
        title: {
            type: String,
            default: "Отправить"
        },
    },
    setup(_, {emit}) {
        const onClick = (() => {
            emit("onClick");
        });
        
        return { onClick };
    }
}
</script>