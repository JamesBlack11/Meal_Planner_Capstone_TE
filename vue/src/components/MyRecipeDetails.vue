<template>
  <div class="recipe-details-body">
      <div class="loading" v-if="isLoading">
    <img src="../assets/your-food-is-being-prepared.gif" />
    </div>
<div class="recipe-details-card">
    <h1 class="recipe-name">{{ recipe.name }}</h1>
</div>



<img class="icon" v-if="recipe.image" v-bind:src="recipe.image"/>

<div>
    <router-link tag="button" class="btn editRecipe" :to="{name:'edit-recipe', params:{userId: $route.query.userId, recipeId:recipe.recipeId}}" v-if="$route.query.userId" >Edit Recipe</router-link>
</div>

<div class="description-styling">
    <h2 class="description">Description</h2>
    <p class="description">{{ recipe.description }}</p>
</div>
<div>
    <h2 class="instructions">Instructions</h2>
    <p class="instruction-body">{{ recipe.instructions }}</p>
</div>
<div>
  
    <h2 class = "ingredients">Ingredients</h2>  
    <table>
        <tr>
            <td class="td-headers">
                Amount
            </td>
            <td class="td-headers">
                Units
            </td>
            <td class="td-headers">
                Name
            </td>
        </tr>
        <tr class="col-name" v-for="ingredient in recipe.ingredients" v-bind:key="ingredient.id">
            <td>
                {{ ingredient.quantity}}

            </td>
            <td>
                {{ingredient.unit}}
            </td>
            <td>
                {{ingredient.name}}
            </td>
        </tr>
    </table>
    <!-- <router-link><button class="edit button"> Edit Recipe </button>
</router-link> -->
<button onclick="window.print();">Print</button>
</div>
  </div>
  
</template>

<script>
import recipeService from '../services/RecipeService';
export default {
    name: "my-recipe-details",
    
    data () {
        return {
            recipe: {},
            isLoading: true,
        }
    },
    created() {
        this.retrieveDetails()
    },
    methods: {
    retrieveDetails() {
        recipeService.getDetails(this.$route.params.recipeId).then(response =>{
            this.recipe = response.data
            this.isLoading = false;
        })
    }
    },

}
</script>
<style>
/* importation of all fonts */
@import url('https://fonts.googleapis.com/css2?family=Hind:wght@300;400&family=Holtwood+One+SC&family=Quicksand:wght@300;400;500&display=swap');

h1 {
    text-align: center;
}

.recipe-details-body{
    margin: 30px;
}
.icon{
    display: block;
    margin-left: auto;
    margin-right: auto;
    height: 200px;
    width: auto;
    position: relative;
    padding: 10px;
    
}

.description-styling > h2 {
    font-weight: 600;
}

.instruction-body, .description{
    font-family: 'Quicksand', sans-serif;
    font-weight: 500;
    white-space: pre;}

table, tr, td {
    border: 1px solid;
    
}

h2{
    font-family: 'Quicksand';
    text-decoration: underline;
}
.td-headers{
    font-weight: 600;
}



</style>