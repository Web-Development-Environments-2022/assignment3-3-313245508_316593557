
<template>
  <div>

      <div :style="{
        'background-image': `url(https://media.istockphoto.com/photos/healthy-flat-lay-of-sliced-vegetables-composition-picture-id1198220441?k=20&m=1198220441&s=612x612&w=0&h=u9Z7_jok37dMOl41oRovtsIyUk_yWDwH_pADOOwSalg=)`,}">
        <br>
        <br>
        <br>
          <h1 class = "title">
            <b>
           Private Recipes
            </b>
            <br>
            <br>
          </h1>
          <br>
      </div>

    <br>
    <br>
    <br>


    <!-- <RecipePreviewList id="privateRecipeID" class="PrivateRecipes center" /> -->

      <div class="private_recipes">
        <RecipePreviewList id="privateRecipeID" class="PrivateRecipes center" />
      </div>

      <!-- <b-container v-if="isEmptyPrivate()">
        <h3 class="title">
          There are no private recipes
        </h3>
      </b-container> -->
  </div>
  
</template>

<script>
import RecipePreviewList from "../components/RecipePreviewList";

  export default {
    name: "private",
    components: {
      RecipePreviewList
    },
    data() {
      return {
        recipes: [], 
        isEmpty: true,
      }
    },

    methods:
    {
    
    isEmptyPrivate()
    {
        console.log("private_is_empty")
        console.log(this.isEmpty)
        return this.isEmpty;
    },

    async getisEmpty(data)
    {
      console.log(data)
      this.isEmpty = data;
    }

    }, 
  }
  
</script>


<style>

.title 
{
  text-align: center;
}





</style>
