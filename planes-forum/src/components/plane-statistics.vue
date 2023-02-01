<script>
import { planeList } from "./plane-list.vue";

export default {
  data() {
    return {
      classificationList: ["Fighter", "Bomber", "Spy"],
    };
  },
  computed: {
    planeStatistics() {
      const statisticsList = {
        Fighter: 0,
        Bomber: 0,
        Spy: 0,
      };
      planeList.forEach((plane) => {
        this.classificationList.forEach((classificationItem) => {
          var temp = plane.classification.indexOf(classificationItem);
          console.log(`${plane.name} - ${classificationItem} - ${temp}`);
          if (plane.classification.indexOf(classificationItem) > -1) {
            statisticsList[classificationItem] += 1;
          }
        });
      });
      return statisticsList;
    },
  },
};
</script>

<template>
  <h3>Plane Statistics</h3>
  <ul>
    <li
      v-for="(item, classification, index) in planeStatistics"
      v-bind:key="`item-${index}`"
    >
      {{ classification }}: {{ item }}
    </li>
  </ul>
</template>
