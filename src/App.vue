<template>
  <!-- RECOMMENDATION: Look at src/components/Penguin.vue, first to see visual feedback -->
  <div id="app">
    <div>
      <h2>List of Penguins</h2>
      <!-- These two buttons are linked to the methods found below -->
      <button @click="moveBestPenguinToTop">Move best penguin to top</button>
      <button @click="moveWorstPenguinToBottom">
        Move worst penguin to bottom
      </button>
      <!-- Visit Penguin.vue and make this data display -->
      <penguin
        v-for="penguin in penguins"
        :key="penguin.name"
        :penguin="penguin"
      />
    </div>

    <div>
      <h2>Best Penguin</h2>
      <penguin :penguin="bestPenguin" />
    </div>

    <div>
      <h2>Worst Penguin</h2>
      <penguin :penguin="worstPenguin" />
    </div>
  </div>
</template>

<script>
import Penguin from "./components/Penguin.vue";
export default {
  name: "App",
  components: {
    Penguin,
  },
  computed: {
    // NOTE: these computed values will be utilized by the Penguin.vue component ( see template )
    bestPenguin() {
      // find the penguin with the highest rating in the array and return it
      // access the penguin list using `this.penguins`
      const penguinArr = this.penguins;
      let bestRate = penguinArr[0].rating;
      let bestPenguin = penguinArr[0];
      penguinArr.map((ele) => {
        if (ele.rating < bestRate) {
          bestRate = ele.rating;
          bestPenguin = ele;
        }
      });
      return bestPenguin;
    },

    worstPenguin() {
      // find the penguin with the lowest rating in the array and return it
      const penguinArr = this.penguins;
      let worstRate = penguinArr[0].rating;
      let worstPenguin = penguinArr[0];
      penguinArr.map((ele) => {
        if (ele.rating > worstRate) {
          worstRate = ele.rating;
          worstPenguin = ele;
        }
      });
      return worstPenguin;
    },
  },

  methods: {
    moveBestPenguinToTop() {
      // move the highest-rated penguin to the top of the list
      // Do not sort the entire array, ONLY move the best penguin
      let bestRate = this.penguins[0].rating;
      let bestIndex = 0;
      this.penguins.forEach((ele, index) => {
        if (ele.rating < bestRate) {
          bestRate = ele.rating;
          bestIndex = index;
        }
      });
      const tempPenguin = {};
      tempPenguin.name = this.penguins[bestIndex].name;
      tempPenguin.rating = this.penguins[bestIndex].rating;
      this.penguins[bestIndex].name = this.penguins[0].name;
      this.penguins[bestIndex].rating = this.penguins[0].rating;
      this.penguins[0].name = tempPenguin.name;
      this.penguins[0].rating = tempPenguin.rating;
    },

    moveWorstPenguinToBottom() {
      // move the worst-rated penguin to the bottom of the list
      // Do not sort the entire array, ONLY move the worst penguin
      let worstRate = this.penguins[0].rating;
      let worstIndex = 0;
      this.penguins.forEach((ele, index) => {
        if (ele.rating > worstRate) {
          worstRate = ele.rating;
          worstIndex = index;
        }
      });
      const tempPenguin = {};
      tempPenguin.name = this.penguins[worstIndex].name;
      tempPenguin.rating = this.penguins[worstIndex].rating;
      this.penguins[worstIndex].name = this.penguins[
        this.penguins.length - 1
      ].name;
      this.penguins[worstIndex].rating = this.penguins[
        this.penguins.length - 1
      ].rating;
      this.penguins[this.penguins.length - 1].name = tempPenguin.name;
      this.penguins[this.penguins.length - 1].rating = tempPenguin.rating;
    },
  },
  data() {
    return {
      penguins: [
        {
          name: "Yellow Eyed",
          rating: 4,
        },
        {
          name: "Humboldt",
          rating: 4,
        },
        {
          name: "Emperor",
          rating: 1,
        },
        {
          name: "King",
          rating: 5,
        },
        {
          name: "Fiordland",
          rating: 2,
        },
        {
          name: "Snares",
          rating: 3,
        },
      ],
    };
  },
};
</script>

<style>
h2 {
  font-size: 20px;
  font-weight: 700;
}
#app {
  padding: 6px 20px;
}
button {
  background: green;
  display: block;
  color: white;
  padding: 8px;
  margin-bottom: 4px;
}
</style>
