<script>
import CounterItem from "./components/counter-item-comp.vue";

export default {
  components: {
    CounterItem,
  },
  data() {
    return {
      message: "Hello it works",
      listOfNumbers: [1, 2, 3, 4, 5],
    };
  },
  watch: {},
};
</script>

<template>
  <CounterItem />
  <counter-item />
  <hr />
  <p v-if="message.length % 2 === 0">Even: {{ message }}</p>
  <p v-else>Odd: {{ message }}</p>
  <ul>
    <li v-for="(number, index) in listOfNumbers" v-bind:key="`number-${index}`">
      {{ number }}
    </li>
  </ul>
</template>
