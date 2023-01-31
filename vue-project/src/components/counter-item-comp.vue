<script>
export default {
  data: () => ({
    count: 10,
    counterTitle: "Counter Standard",
    incrementAmount: 1,
  }),
  computed: {
    displayTitle() {
      if (this.count < 20) {
        return "Counter Standard";
      } else {
        return "Counter Standatd - Very Long";
      }
    },
    optimizedIncrementAmount() {
      return this.displayTitle.length * this.incrementAmount;
    },
  },
  methods: {
    incrementCounter() {
      this.count += this.incrementAmount;
    },
    decrementCounter() {
      this.count -= this.incrementAmount;
    },
  },
};
</script>

<template>
  <h1>{{ displayTitle }}</h1>
  <p>{{ count }}</p>
  <p>{{ optimizedIncrementAmount }}</p>
  <button v-on:click="incrementCounter">Increment Counter</button>
  <br />
  <button v-on:click="decrementCounter">Decrement Counter</button>
  <br />
  <h2>{{ incrementAmount }}</h2>
  <label for="incrementAmount">Increment by:</label>
  <input type="number" v-model="incrementAmount" />
</template>
