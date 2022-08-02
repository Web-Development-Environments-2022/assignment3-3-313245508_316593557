
<template>
  <div>
  <b-container>
    <div :style="{
        'background-image': `url(https://media.istockphoto.com/photos/healthy-flat-lay-of-sliced-vegetables-composition-picture-id1198220441?k=20&m=1198220441&s=612x612&w=0&h=u9Z7_jok37dMOl41oRovtsIyUk_yWDwH_pADOOwSalg=)`,}">
    <br><br><br>

      <h1 class = "title">
        <b>
        Family Recipes
        </b>
        <br><br>
      </h1>
        <br>
    </div>
<br><br><br>
      <div class="family_recipes">
        <RecipePreviewList id="familyRecipeID" class="FamilyRecipes center" />
      </div>

    </b-container>

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
}

</style>