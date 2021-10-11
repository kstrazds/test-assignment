<template>
    <div class="field question-field">
        <label :class="['input-label', {required: questionRequired}]"
               :for="questionCode">
            {{ questionName }}
        </label>
        <p class="question-description" v-if="descriptionStatus">{{ questionDescription }}</p>
        <select class="question-select" :type="questionType" :name="questionName" :id="questionCode">
            <option v-for="(value, keys) in questionChoices" :key="keys" :value="keys">
                <!-- This part for the span - probably should be achieved in a different manner -->
                <span v-for="answer in value" :key="answer">{{ answer }}</span>
            </option>
        </select>
    </div>
</template>

<script>
    export default {
        name: "Questions",
        props: {
            questionName: {
                type: String
            },
            questionType: {
                type: String
            },
            questionCode: {
                type: String
            },
            questionRequired: {
                type: Boolean
            },
            questionDescription: {
                type: String
            },
            questionChoices: {
                type: Array
            }
        },
        computed: {
            descriptionStatus() {
                return this.questionDescription !== "";
            }
        }
    }
</script>
