
<template>
  <div>

      <div :style="{
        'background-image': `url(https://static2.bigstockphoto.com/7/9/2/large1500/297327124.jpg)`,}">
    <br><br><br><br><br>

          <h1 class = "title">
            <b>
           Private Recipes
            </b>
        <br><br><br>

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
  color: rgb(255, 255, 255);
}





</style>
