<template>
  <div class="my-recipes">
    <div class="loading" v-if="isLoading">
      <img id="loading-image" src="../assets/cooking-bear.gif" />
    </div>
    <div v-else>
    <div class="recipe-header">
      <h1>My Recipe Library</h1>
    </div>

    <router-link
      tag="button"
      class="btn addNewRecipe"
      :to="{ name: 'add-recipe', params: { userId: $route.params.id } }"
      v-if="!isLoading"
      >Add New Recipe</router-link
    >

    <recipe-card
      v-for="recipe in myRecipes"
      v-bind:userId="$route.params.id"
      v-bind:key="recipe.name"
      v-bind:recipe="recipe"
    />
  </div>
  </div>
</template>

<script>
import RecipeCard from "@/components/RecipeCard.vue";
import recipeService from "@/services/RecipeService";

export default {
  name: "my-recipes",
  components: { RecipeCard },
  data() {
    return {
      myRecipes: [],
      isLoading: true,
    };
  },
  created() {
    this.retrieveMyRecipes();
  },

  methods: {
    retrieveMyRecipes() {
      recipeService.getMyRecipes(this.$route.params.id).then((response) => {
        this.myRecipes = response.data;
        this.isLoading = false;
      });
    },
  },
};
</script>

<style>
#loading-image {
  display: block;
  margin-left: auto;
  margin-right: auto;
}

.my-recipes {
  width: 90%;
  margin: 50px auto;
}

.recipe-header {
  text-align: center;
  font-size: 20px;
  color: rgb(168, 64, 64);
  margin-bottom: 40px;
}
/* .recipe-row{
    display: flex;
  flex-direction: row;
  justify-content: flex-start;
  gap: 3px;
  flex-flow: wrap;
  margin-left: 40px;
} */
.recipe-row #p {
  border-bottom: 10px, solid;
}
</style>