<template>
  <div id="app">
    <div class="container">
      <Quiz
          v-if="!finish"
          :birdsData="birds"
          :randomValue="randomValue"
      />
      <Result v-else />
    </div>
    <!--<div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>-->
  </div>
</template>

<script>
  import Quiz from '@/views/Quiz.vue'
  import Result from '@/views/Result.vue'

  export default {
    name: 'App',
    data() {
      return {
        birds: [],
        finish: false,
        randomValue: null,
      }
    },
    components: {
      Quiz,
      Result
    },
    created: function() {
      this.randomValue = Math.floor(Math.random() * (5 + 1));

      axios.get(' ./birds.json')
        .then((response) => {
          this.birds = response.data.birds;
          console.log(this.birds);
      });
    }
  }
</script>

<style lang="scss">


/*#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}*/
</style>
