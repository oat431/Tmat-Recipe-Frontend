<template>
  <div
    class="max-w-xs mx-auto overflow-hidden bg-white rounded-lg shadow-lg dark:bg-gray-800 mt-6"
  >
    <div class="px-4 py-2">
      <h1 class="text-3xl font-bold text-gray-800 uppercase dark:text-white">
        {{ this.Recipe.title }}
      </h1>
      <p class="mt-1 text-sm text-gray-600 dark:text-gray-400">
        {{ this.Recipe.instructions[1] }}
      </p>
    </div>

    <img
      class="object-cover w-full h-48 mt-2"
      :src="'../food_image/' + this.Recipe.image_Name + '.jpg'"
      :alt="this.Recipe.image_Name"
    />
    <div class="flex items-center justify-between px-4 py-2 bg-gray-900">
      <!-- <h1 class="text-lg font-bold text-white">see more</h1> -->
      <router-link
        class="text-lg font-bold text-green-100"
        :to="'/details/' + this.Recipe.id"
        >See more</router-link
      >
      <button
        v-if="!GlobalState.markIndex.includes(this.Recipe.id.toString())"
        class="px-2 py-1 text-xs font-semibold text-gray-900 uppercase transition-colors duration-200 transform bg-white rounded hover:bg-gray-200 focus:bg-gray-400 focus:outline-none"
        @click="markRecipe"
      >
        Save
      </button>
      <button
        v-else
        class="px-2 py-1 text-xs font-semibold text-gray-900 uppercase transition-colors duration-200 transform bg-white rounded hover:bg-gray-200 focus:bg-gray-400 focus:outline-none"
        @click="unmarkRecipe"
      >
        delete
      </button>
    </div>
  </div>
</template>

<script>
import FoodAPI from "../services/FoodAPI.js";
export default {
  props: ["Recipe"],
  inject: ["GlobalState"],
  methods: {
    markRecipe() {
      FoodAPI.markingRecipe(this.GlobalState.currentUser.id, this.Recipe.id)
        .then((res) => {
          console.log(res);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    unmarkRecipe() {
      FoodAPI.unmarkingRecipe(this.GlobalState.currentUser.id, this.Recipe.id)
        .then((res) => {
          console.log(res);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
