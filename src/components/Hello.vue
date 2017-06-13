<template lang="pug">
  v-card(v-if="win")
    v-card-text
     p
      | Ура ты выигарал, и загадала
      b {{number}}
    v-btn(@click.native="newGame") Играть еще раз!
  v-card(v-else)
    v-card-text
      div Я загадала номер от 0 до 100, тебе нужно угадать.
    v-layout(row wrap)
      v-flex(xs2)
        v-btn(v-for="i in lastChoose", :key="i", primary).white--text {{i}}
      v-flex(xs10)
        v-btn(v-for="i in range", :key="i", @click.native="onChoose(i)") {{i}}
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      number: 0,
      lastChoose: [],
      minChoose: 0,
      maxChoose: 101,
      win: false
    }
  },
  created () {
    this.newGame()
  },
  computed: {
    range () {
      return [...this.rangeGen(this.minChoose + 1, this.maxChoose - 1)]
    }
  },
  methods: {
    newGame () {
      this.number = this.getRandomInt(1, 100)
      this.minChoose = 0
      this.maxChoose = 101
      this.win = false
      this.lastChoose = []
    },
    getRandomInt (min, max) {
      return Math.floor(Math.random() * (max - min)) + min
    },
    onChoose (choose) {
      this.lastChoose.push(choose)
      if (this.number > choose) {
        this.minChoose = choose
      } else if (this.number < choose) {
        this.maxChoose = choose
      } else {
        this.win = true
      }
    },
    *rangeGen (begin, end) {
      for (let i = begin; i <= end; i++) {
        yield i
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
