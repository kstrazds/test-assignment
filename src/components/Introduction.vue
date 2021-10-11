<template>
    <div class="introduction">
        <div class="page-title">
            <h1>{{ quizTitle }}</h1>
        </div>
        <div class="page-subtitle">
            <p v-html="quizSubtitle"/>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Introduction",
        props: {
            quizTitle: {
                type: String
            },
            quizSubtitle: {
                type: String
            }
        }
    }
</script>
