<template>
  <div id="app">
    <p>{{message}}</p>
    <div class="counter-container">
      <h1>{{transformDate(time)}}</h1>
    </div>
    <div class="button-container">
      <button v-if="!started" @click="startCounting">
        <i class="far fa-play-circle"></i>
      </button>
      <button v-else @click="pauseCounting">
        <i class="far fa-pause-circle"></i>
      </button>
      <button v-if="!compareDates()" @click="restartCounting">
        <i class="fas fa-undo-alt"></i>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      time: new Date(2019, 1, 20, 9, 25, 0, 0),
      count: null,
      started: false,
      message: "Let the count begin!"
    };
  },
  methods: {
    startCounting() {
      this.started = !this.started;
      this.message = "Greatness is within sight!!";
      this.count = setInterval(this.counting, 1000);
    },
    transformDate(time) {
      return time.toLocaleTimeString(navigator.language, {
        minute: "2-digit",
        second: "2-digit"
      });
    },
    counting() {
      var diff = this.time.getTime() - 1000;
      this.time = new Date(diff);
    },
    pauseCounting() {
      this.started = !this.started;
      this.message = "Never quit, keep going!!";
      clearInterval(this.count);
    },
    restartCounting() {
      this.started = false;
      this.message = "Let the count begin!";
      clearInterval(this.count);
      this.time = new Date(2019, 1, 20, 9, 25, 0, 0);
    },
    compareDates() {
      return (
        this.time.getTime() === new Date(2019, 1, 20, 9, 25, 0, 0).getTime()
      );
    }
  }
};
</script>

<style lang="scss">
body {
  margin: 0;
  padding: 0;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 100%;
  height: 100vh;
  background: #05a1de;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  p {
    color: white;
    margin: 0;
  }

  .counter-container {
    color: white;
    h1 {
      font-size: 12rem;
      margin: 0;
    }
  }

  .button-container {
    button {
      border: none;
      padding: 0.75rem 1rem;
      font-size: 1.5rem;
      border-radius: 5px;
      background: #343734;
      color: white;
      cursor: pointer;
      margin-right: 1.5rem;
    }
  }
}
</style>
