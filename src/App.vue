<template>
<div class="root" :style="{backgroundColor}">
  <button class="button" @click="updateScore" :style="{borderBottom}">
    {{score}}
  </button>
  <button ref="root"  class="test">
  </button>
</div>
</template>

<script>
export default {
  name: 'App',
  computed: {
    backgroundColor() {
      const speed = 3
      const color = this.score % (360 / speed)
      return `hsl(${color * speed}, 50%, 55%)`
    },
    borderBottom() {
      const speed = 3
      const color = this.score % (360 / speed)
      return `15px solid hsl(${color * speed}, 55%, 25%)`
    }
  },
  data() {
    return {
      score: 0
    }
  },
  mounted() {
    this.loadScore()
  },
  methods:{
    loadScore() {
      const score = localStorage.getItem('score') || 0
      this.score = +score
    },
    updateScore() {
      localStorage.setItem('score', ++this.score)
      setTimeout(() => {
        this.$refs.root.focus()
      }, 100);
    }
  }
}

</script>

<style lang="scss">
@import url('~@fortawesome/fontawesome-free/css/all.min.css');
@import url('./assets/font/jost.css');
body {
  background-color: black;
  margin: 0;
  color: white;
  overflow: auto;
  font-family: 'Jost';
}

.root {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100vw;
  transition: 300ms;
  button {
    color: white;
    background-color: #fff;
    width: 0;
    height: 0;
    position: absolute;
    z-index: -1;
  }
  button.button {
    font-family: 'Jost';
    font-weight: 100;
    border: none;
    z-index: 1;
    background-color: white;
    width: 50vw;
    height: 50vw;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: calc(50vw / 3);
    border-radius: 25%;
    border-bottom: 15px solid black;
    transition: 100ms;
    color: black;
    outline: none;
    &:focus {
      border-bottom-width: 0 !important;
      transform: scale(0.98);
    }
  }
}
</style>
