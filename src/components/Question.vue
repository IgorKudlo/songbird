<template>
  <div class="question">
    <div class="random-bird jumbotron rounded">
      <img class="bird-image" src="../assets/bird.jpg" alt="bird" v-if="!correctAnswer">
      <img class="bird-image" :src="birds[currentQuestion - 1][randomValue].image" :alt="birds[0][randomValue].name" v-else>
      <div>
        <ul class="list-group list-group-flush">
          <li class="list-group-item">
            <h3 v-if="!correctAnswer">******</h3>
            <h3 v-else>{{ birds[currentQuestion - 1][randomValue].name }}</h3>
          </li>
          <li class="list-group-item">
            <div class="audio-player">
              <audio controls>
                <source :src="birds[currentQuestion - 1][randomValue].audio" type="audio/mpeg">
                Your browser does not support the audio element.
              </audio>
            </div>
          </li>
        </ul>
      </div>
    </div>
    <div class="row mb2">
      <div class="col-md-6">
        <ul class="item-list list-group">
          <li class="list-group-item" v-for="(bird, index) of birds[currentQuestion - 1]" @click="choiceOption(index)">
            <span class="li-btn"></span>{{ bird.name }}
          </li>
        </ul>
      </div>
      <div class="col-md-6">
        <div class="bird-details card">
          <p class="instruction" v-if="!choiceAnswerIndex">
            <span>Послушайте плеер.</span>
            <span>Выберите птицу из списка</span>
          </p>
          <div v-else>
            <div class="card-body">
              <img class="bird-image" :src="birds[currentQuestion - 1][choiceAnswerIndex].image" :alt="birds[currentQuestion - 1][choiceAnswerIndex].name">
              <ul class="list-group list-group-flush">
                <li class="list-group-item">
                  <h4>{{ birds[currentQuestion - 1][choiceAnswerIndex].name }}</h4>
                </li>
                <li class="list-group-item">
                  <span>{{ birds[currentQuestion - 1][choiceAnswerIndex].species }}</span>
                </li>
                <li class="list-group-item">
                  <div class="audio-player">
                    <audio controls>
                      <source :src="birds[currentQuestion - 1][choiceAnswerIndex].audio" type="audio/mpeg">
                      Your browser does not support the audio element.
                    </audio>
                  </div>
                </li>
              </ul>
            </div>
            <span class="bird-description">{{ birds[currentQuestion - 1][choiceAnswerIndex].description }}</span>
          </div>
        </div>
      </div>
      <button class="btn" :class="{ 'btn-next': correctAnswer}" @click="nextQuestion">Next Level</button>
    </div>
  </div>
</template>

<script>
  export default {
    name: "Question",
    props: ['birds'],
    data() {
      return {
        correctAnswer: false,
        currentQuestion: 1,
        choiceAnswerIndex: null,
        randomValue: null,
      }
    },
    methods: {
      choiceOption(index) {
        this.correctAnswer = index === this.randomValue;
        this.choiceAnswerIndex = index.toString();
      },
      nextQuestion() {
        if(this.correctAnswer) {
          this.currentQuestion += 1;
          this.randomValue = Math.floor(Math.random() * (5 + 1));
          this.correctAnswer = false;
          this.choiceAnswerIndex = null;
        }
      }
    },
    created: function() {
      this.randomValue = Math.floor(Math.random() * (5 + 1));
    }
  }
</script>
