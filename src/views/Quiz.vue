<template>
  <div class="home">
    <Header/>
    <Question
        :birds="birdsData"
        :randomValue="randomValue"
    />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Question from "@/components/Question.vue"

export default {
  name: 'Quiz',
  props: ['birdsData', 'randomValue'],
  components: {
    Header,
    Question
  }
}
</script>
