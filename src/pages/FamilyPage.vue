
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
<<<<<<< HEAD
        <RecipePreviewList id="familyRecipeID" class="FamilyRecipes center" />
      </div>

=======
        <FamilyRecipePreviewList id="familyRecipeID" class="FamilyRecipes center" />
      </div>

      <!-- <div class="family_recipes">
        <div class="family_recipes" v-for="r in recipes" :key="r.id">
            <RecipePreview class="recipePreview" :recipe="r" />
        </div>
      </div> -->

        <!-- <b-container v-if="isEmptyFamily()">
      <h3 class="title">
        There are no family recipes
      </h3>
        </b-container> -->
>>>>>>> b4f386a786884e3347814d8f794fe2aaaef95d86
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