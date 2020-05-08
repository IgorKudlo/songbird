<template>
  <div class="header d-flex">
    <div class="top-panel d-flex">
      <div class="logo">
        <img alt="logo" src="../assets/logo.svg">
      </div>
      <h5>Score: <span class="score">{{ score }}</span></h5>
    </div>
    <ul class="pagination">
      <li class="page-item active" v-for="link of nav">
        <a class="page-link" href="/#">{{ link }}</a>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'Header',
    data() {
      return {
        score: 0,
        nav: ['Разминка', 'Воробьиные', 'Лесные птицы', 'Певчие птицы', 'Хищные птицы', 'Морские птицы']
      }
    }
  }
</script>
