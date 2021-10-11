<template>
  <div id="app">
    <div class="quiz-container">
      <div class="project-logo-wrapper">
        <img class="project-logo" alt="Project Logo" src="@/assets/logo/project_logo.svg">
      </div>
      <div v-if="!isLastPage" class="quiz-form">
        <div class="introduction-wrapper">
          <Introduction :quiz-title="json.title"
                        :quiz-subtitle="json.pages[page].subttitle"/>
          <ProgressBar :questions-total="questionsCount"
                       :questions-current="answeredQuestions"/>
        </div>
        <div class="questions-wrapper">
          <Questions v-for="data in json.pages[page].questions"
                     :key="data.code"
                     :question-name="data.name"
                     :question-type="data.type"
                     :question-code="data.code"
                     :question-description="data.public_description"
                     :question-choices="data.choices"
                     :question-required="data.is_required"/>
        </div>
        <div class="buttons-wrapper">
          <Buttons :button-forward="buttonCurrentLabel"
                   :button-backwards="json.page_prev_text"
                   :page-number="page"
                   :page-count="json.pages.length - 1"
                   @next-page="getNextPage"
                   @previous-page="getPreviousPage"/>
        </div>
      </div>
      <div v-else class="quiz-summary">
        <FinalPage :completed-heading="json.completed_heading"
                   :completed-text="json.completed_text"/>
      </div>
    </div>
  </div>
</template>

<script>
  import {data} from './survey.json'
  import Introduction from "./components/Introduction";
  import Questions from "./components/Questions";
  import Buttons from "./components/Buttons";
  import FinalPage from "./components/FinalPage";
  import ProgressBar from "./components/ProgressBar";

  export default {
    name: 'App',
    components: {
      Introduction,
      Questions,
      Buttons,
      FinalPage,
      ProgressBar
    },
    data() {
      return {
        json: data,
        page: 0,
        isLastPage: false,
        answeredQuestions: 0
      };
    },
    created() {
      this.answeredQuestions += this.questionsCurrentPage;
    },
    computed: {
      buttonCurrentLabel() {
        if (this.page === this.json.pages.length - 1) {
          return this.json.complete_text;
        }

        return this.json.page_next_text;
      },
      questionsCount() {
        const pagesCount = this.json.pages.length;
        let totalQuestions = 0;

        for (let index = 0; index < pagesCount; index++) {
          totalQuestions += this.json.pages[index].questions.length;
        }

        return totalQuestions;
      },
      questionsCurrentPage() {
        return this.json.pages[this.page].questions.length;
      }
    },
    methods: {
      getNextPage(pageNumber) {
        if (this.page === pageNumber && this.page < this.json.pages.length - 1) {
          this.page++;
          this.answeredQuestions += this.questionsCurrentPage;
          return;
        }

        this.isLastPage = true
      },
      getPreviousPage (pageNumber) {
        if (this.page === pageNumber && this.page !== 0) {
          this.answeredQuestions -= this.questionsCurrentPage;
          this.page--;
        }
      }
    }
  }
</script>

<style lang="scss">
  #app {
    margin: 0;
  }
</style>
