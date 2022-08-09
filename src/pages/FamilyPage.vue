
<template>
  <div>
    <div :style="{
        'background-image': `url(https://static2.bigstockphoto.com/7/9/2/large1500/297327124.jpg)`,}">
    <br><br><br><br><br>

      <h1 class = "title">
        <b>
        Family Recipes
        </b>
        <br><br><br>
      </h1>
        <br>
    </div>
<br><br><br>
      <div class="family_recipes">
        <FamilyRecipePreviewList id="familyRecipeID" class="FamilyRecipes center" />
      </div>


  </div>

  
</template>

<script>
// import RecipePreview from "../components/RecipePreview";
import FamilyRecipePreviewList from "../components/FamilyRecipePreviewList.vue";


  export default {
    name: "family",
    components: {
    // RecipePreview
    FamilyRecipePreviewList
},
    data() {
      return {
        recipes: [], 

      }
    },
    // mounted() 
    // {
    // this.showFamilyRecipes();  
    // },
    methods:
    {
    
    
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