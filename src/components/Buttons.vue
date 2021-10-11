<template>
    <div class="actions-toolbar">
        <div class="button-backwards">
            <button @click="pagePrevious"
                    class="action secondary"
                    :disabled="isDisabled">
                <span>{{ buttonBackwards }}</span>
            </button>
        </div>
        <div class="button-forward">
            <button @click="pageNext"
                    class="action primary">
                <span>{{ buttonForward }}</span>
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Buttons",
        props: {
            buttonForward: {
                type: String
            },
            buttonBackwards: {
                type: String
            },
            pageNumber: {
                type: Number
            },
            pageCount: {
                type: Number
            },

        },
        computed: {
            isDisabled() {
                return this.pageNumber === 0;
            }
        },
        methods: {
            pageNext() {
                this.$emit('next-page', this.pageNumber);
            },
            pagePrevious() {
                this.$emit('previous-page', this.pageNumber);
            }
        }
    }
</script>
