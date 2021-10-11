<template>
    <div class="progress-bar-wrapper">
        <div class="progress-bar-action"
             :style="{width: currentStepPercentage + '%'}"></div>
        <span class="progress-percentage">{{ currentStepPercentage }}%</span>
    </div>
</template>

<script>
    export default {
        name: "ProgressBar",
        props: {
            questionsTotal: {
                type: Number
            },
            questionsCurrent: {
                type: Number
            }
        },
        computed: {
            currentStepPercentage() {
                const calcOnePercent = (100 / this.questionsTotal).toFixed(2);

                return (calcOnePercent * this.questionsCurrent).toFixed(0);
            }
        }
    }
</script>
