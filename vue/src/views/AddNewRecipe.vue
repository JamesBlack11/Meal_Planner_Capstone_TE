<template>
  <div class=addNewRecipe>
      <h1>Add New Recipe</h1>
      <add-new-recipe-form></add-new-recipe-form>
    
  </div>
</template>

<script>
import AddNewRecipeForm from "@/components/AddNewRecipeForm";

export default {
    components: {
        AddNewRecipeForm
    }

}
</script>

<style>
.addNewRecipe{
    background-color: lavender;
}

</style>