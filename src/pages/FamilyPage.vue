
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
import RecipePreviewList from "../components/RecipePreviewList";


  export default {
    name: "family",
    components: {
      // RecipePreview
      RecipePreviewList
    },
    data() {
      return {
        recipes: [], 
        isEmpty: true,
      }
    },
    // mounted() 
    // {
    // this.showFamilyRecipes();  
    // },
    methods:
    {
    //   async showFamilyRecipes()
    // {
    //     try{
    //       let response = await this.axios.get(
    //         this.$root.store.server_domain + "/users/family",{
    //           params: 
    //           {

    //           }
    //         }
    //       );
    //       if(response == []) // there are no family recipes for the specific user
    //       {
    //         return;
    //       }
    //       else
    //       {
    //         isEmpty = false;
    //         const searchResults = response.data;
    //         this.recipes = [];
    //         this.recipes.push(...searchResults);
    //       }
          

    //     } catch (err)
    //     {
    //       console.log("got err")
    //       console.log(err.response);
    //     }
    //   },
    isEmptyFamily()
    {
        return this.isEmpty;
    },

    async getisEmpty(data)
    {
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