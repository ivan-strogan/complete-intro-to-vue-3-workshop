<script>
export default {
  data() {
    return {
      count: 10,
      counterTitle: "Counter Standard",
      incrementAmount: 1,
      message: "Hello it works",
      listOfNumbers: [1, 2, 3, 4, 5],
    };
  },
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
  watch: {},
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
  <hr />
  <p v-if="message.length % 2 === 0">Even: {{ message }}</p>
  <p v-else>Odd: {{ message }}</p>
  <ul>
    <li v-for="(number, index) in listOfNumbers" v-bind:key="`number-${index}`">
      {{ number }}
    </li>
  </ul>
</template>
