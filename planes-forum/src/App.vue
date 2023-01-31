<script>
export default {
  data() {
    return {
      newPlane: {
        name: "",
        classification: [],
      },
      classificationList: ["Fighter", "Bomber", "Spy"],
      planeList: [
        {
          name: "F-16",
          classification: ["Fighter"],
        },
        {
          name: "Mig-29",
          classification: ["Fighter"],
        },
        {
          name: "Su-27",
          classification: ["Fighter", "Bomber"],
        },
        {
          name: "Tu-24",
          classification: ["Bomber"],
        },
        {
          name: "U-2",
          classification: ["Spy"],
        },
      ],
      favoriteList: [],
    };
  },
  computed: {
    planeStatistics() {
      const statisticsList = {
        Fighter: 0,
        Bomber: 0,
        Spy: 0,
      };

      this.planeList.forEach((plane) => {
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
  methods: {
    addPlaneToList() {
      if (
        this.newPlane !== "" &&
        this.planeList.map((e) => e.name).includes(this.newPlane) !== true
      ) {
        this.planeList.push({
          name: this.newPlane,
        });
        // console.log(this.planeList)
        this.planeList = this.sortList(this.planeList);
        // console.log(this.planeList)
      }
      this.newPlane = "";
      this.save();
    },
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
      localStorage.planeList = JSON.stringify(this.planeList);
    },
    sortList(list) {
      return list.sort((a, b) => {
        return a["name"].localeCompare(b["name"]);
      });
    },
  },
  mounted() {
    if (localStorage.planeList) {
      this.planeList = JSON.parse(localStorage.planeList);
    }
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
  <hr />
  <h3>Plane Statistics</h3>
  <ul>
    <li
      v-for="(item, index, classification) in planeStatistics"
      v-bind:key="`item-${index}`"
    >
      {{ classification }}: {{ item }}
    </li>
  </ul>
  <hr />
  <h3>List of Planes</h3>
  <p v-if="planeList.length === 0">There are no planes listed.</p>
  <div v-else>
    <ul>
      <li v-for="(plane, index) in planeList" v-bind:key="`plane-${index}`">
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
