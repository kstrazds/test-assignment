<template>
    <div class="quiz-complete">
        <div class="page-title">
            <h1>{{ completedHeading }}</h1>
        </div>
        <div class="page-subtitle">
            <p>{{ completedText }}</p>
        </div>
    </div>
</template>

<script>
    export default {
        name: "FinalPage",
        props: {
            completedText: {
                type: String
            },
            completedHeading: {
                type: String
            }
        }
    }
</script>
