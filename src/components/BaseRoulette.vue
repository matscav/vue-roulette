<template>
  <div class="container">
    <div class="roulette">
      <div class="user" :class="isSelected(index)" v-for="(user, index) in users" :key="index">
        {{ user }}
      </div>
    </div>
    <button class="spin-button" @click="spinRoulette">Spin!</button>
  </div>
</template>

<script>
export default {
  name: 'BaseRoulette',
  data () {
    return {
      users: ['bruno', 'jose javier', 'carmen', 'juan pablo', 'roberto', 'adrian antonio', 'simon', 'sergio', 'ismael', 'irina', 'ricardo adrian', 'dario', 'lucia', 'carlos', 'antonio', 'mathias', 'nestor', 'aythami'],
      userSelected: -1
    };
  },
  methods: {
    getRandom () {
      return Math.floor(Math.random() * this.users.length);
    },
    spinRoulette () {
      if (this.userSelected !== -1) {
        this.$el.querySelector('.selected').classList.remove('super-selected');
      }
      const selectionInterval = setInterval(() => {
        this.userSelected = this.getRandom();
      }, 200);
      setTimeout(() => {
        clearInterval(selectionInterval);
        this.$el.querySelector('.selected').classList.add('super-selected');
      }, 5000);
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
  }
}
</style>
