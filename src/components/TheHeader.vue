<template>
    <header class="header">
        <div class="header__wrapper">
            <h2 class="header__title">{{ app.title }}</h2>
        </div>
    </header>
</template>

<script>
import { app } from "@/_config.js"
export default {
    setup() {
        return {app};
    },
}
</script>