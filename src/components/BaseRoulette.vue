<template>
  <div class="container">
    <div class="roulette">
      <div class="user" :class="isSelected(index)" v-for="(user, index) in users" :key="index">
        {{ user }}
      </div>
    </div>
    <button class="spin-button" @click="spinRoulette" :disabled="isLoading">
        <span v-show="!isLoading">Spin!</span>
        <SyncLoader :loading="isLoading" color="green" size="30px" />
      </button>
  </div>
</template>

<script>
import SyncLoader from './SyncLoader.vue';
export default {
  name: 'BaseRoulette',
  components: {
    SyncLoader
  },
  data () {
    return {
      users: ['bruno', 'jose javier', 'carmen', 'juan pablo', 'roberto', 'adrian antonio', 'simon', 'sergio', 'ismael', 'irina', 'ricardo adrian', 'dario', 'lucia', 'carlos', 'antonio', 'mathias', 'nestor', 'aythami'],
      userSelected: -1,
      winnerSound: new Audio('https://freesound.org/data/previews/435/435878_1992856-lq.mp3'),
      isLoading: false
    };
  },
  methods: {
    getRandom () {
      return Math.floor(Math.random() * this.users.length);
    },
    spinRoulette () {
      this.isLoading = true;
      if (this.userSelected !== -1) {
        this.$el.querySelector('.selected').classList.remove('super-selected');
      }
      const selectionInterval = setInterval(() => {
        this.userSelected = this.getRandom();
      }, 200);
      setTimeout(() => {
        this.winnerSound.play();
        setTimeout(() => {
          clearInterval(selectionInterval);
          this.voiceSynthesis(this.users[this.userSelected]);
          this.$el.querySelector('.selected').classList.add('super-selected');
          this.isLoading = false;
        }, 2250);
      }, 3000);
    },
    voiceSynthesis (text) {
      const utterance = new SpeechSynthesisUtterance(text);
      speechSynthesis.speak(utterance);
    },
    isSelected (index) {
      return (index === this.userSelected) ? 'selected' : '';
    }
  }
};
</script>

<style lang="postcss">
@keyframes createBox {
  from {
    transform: scale(1);
  }
  to {
    transform: scale(2);
  }
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 50%;
  margin: auto;
  & .roulette {
    border: 2px solid red;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    width: 100%;
    margin: auto;
    & .user {
      border: 2px solid black;
      margin:6px;
      padding: 6px;
      font-size: 36px;
      text-transform: capitalize;
    }
    & .selected {
      background: lightgreen;
    }
    & .super-selected {
      background: green;
      animation: createBox 1s;
    }
  }
  & .spin-button {
    margin-top: 25px;
    padding: 20px;
    font-size: 40px;
    cursor: pointer;
  }
  & .spin-button:disabled {
    cursor: wait;
  }
}
</style>
