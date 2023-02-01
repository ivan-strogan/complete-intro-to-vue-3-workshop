<script>
import { planeList, setPlaneList } from "./plane-list.vue";

export default {
  data() {
    return {
      newPlane: {
        name: "",
        classification: [],
      },
    };
  },
  methods: {
    addPlaneToList() {
      if (
        this.newPlane !== "" &&
        planeList.map((e) => e.name).includes(this.newPlane) !== true
      ) {
        let updatedPlaneList = planeList;
        updatedPlaneList.push({
          name: this.newPlane,
        });

        setPlaneList(updatedPlaneList);
        // console.log(this.planeList)
        updatedPlaneList = this.sortList(updatedPlaneList);
        // console.log(this.planeList)
      }
      this.newPlane = "";
      this.save();
    },
    save() {
      localStorage.planeList = JSON.stringify(planeList);
    },
    sortList(list) {
      return list.sort((a, b) => {
        return a["name"].localeCompare(b["name"]);
      });
    },
  },
};
</script>

<template>
  <form @submit.prevent="addPlaneToList">
    <label for="newPlane">Add plane to the plane list.</label>
    <input type="text" v-model="newPlane.name" />
    <input type="text" v-model="newPlane.classification" />
    <br />
    <button>Add Plane</button>
  </form>
</template>
