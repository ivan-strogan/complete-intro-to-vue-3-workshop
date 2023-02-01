<script>
import AddPlane from "./components/add-plane.vue";
import PlaneStatistics from "./components/plane-statistics.vue";
import { planeList } from "./components/plane-list.vue";

export default {
  components: {
    AddPlane,
    PlaneStatistics,
  },
  data() {
    return {
      favoriteList: [],
      planeListInternal: planeList,
    };
  },
  methods: {
    addToFavoriteList(planeName) {
      this.favoriteList.push({ name: planeName });
      this.save;
    },
    removeFromFavoriteList(planeName) {
      const index = this.favoriteList.map((e) => e.name).indexOf(planeName);
      this.favoriteList.splice(index, 1);
      this.save;
    },
    save() {
      // localStorage.planeList = JSON.stringify(planeList);
    },
    sortList(list) {
      return list.sort((a, b) => {
        return a["name"].localeCompare(b["name"]);
      });
    },
  },
  mounted() {
    if (localStorage.planeList) {
      // planeList = JSON.parse(localStorage.planeList);
    }
  },
};
</script>

<template>
  <AddPlane />
  <hr />
  <PlaneStatistics />
  <hr />
  <h3>List of Planes</h3>
  <p v-if="planeListInternal.length === 0">There are no planes listed.</p>
  <div v-else>
    <ul>
      <li
        v-for="(plane, index) in planeListInternal"
        v-bind:key="`plane-${index}`"
      >
        {{ plane.name }} -
        <button
          v-if="favoriteList.map((e) => e.name).includes(plane.name)"
          @click="removeFromFavoriteList(plane.name)"
        >
          Remove from Favorite List
        </button>
        <button v-else @click="addToFavoriteList(plane.name)">
          Add to Favorite List
        </button>
      </li>
    </ul>
  </div>
  <hr />
  <h3>List Of Favorite Planes</h3>
  <p v-if="favoriteList.length === 0">
    There are no planes in your favorites list.
  </p>
  <div v-else>
    <ul>
      <li
        v-for="(favorite, index) in favoriteList"
        v-bind:key="`favorite-${index}`"
      >
        {{ favorite.name }}
      </li>
    </ul>
  </div>
</template>
