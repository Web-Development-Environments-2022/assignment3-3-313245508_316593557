
<template class="aaa">
      <div>
    <div :style="{
        'background-image': `url(https://media.istockphoto.com/photos/healthy-flat-lay-of-sliced-vegetables-composition-picture-id1198220441?k=20&m=1198220441&s=612x612&w=0&h=u9Z7_jok37dMOl41oRovtsIyUk_yWDwH_pADOOwSalg=)`,}">
    <br><br><br>

      <h1 class = "title">
        <b>
        Favorite Recipes
        </b>
        <br><br>
      </h1>
        <br>
    </div>

<br><br><br>

      <div class="favorites_recipes">
        <RecipePreviewList id="favoriteRecipeID" class="FavoritesRecipes center" />
      </div>
  </div>

  
</template>

<script>
// import RecipePreview from "../components/RecipePreview";
import RecipePreviewList from "../components/RecipePreviewList";

  export default {
    name: "favorites",
    components: {
      // RecipePreview
      RecipePreviewList
    },
    data() {
      return {
        recipes: [], 
        // isEmpty: true,
      }
    },
    // mounted() 
    // {
    // this.showFavoriteRecipes();  
    // },
    methods:{
    //   async showFavoriteRecipes()
    // {
    //     try{
    //       let response = await this.axios.get(
    //         this.$root.store.server_domain + "/users/favorites",
    //       );

    //       response = JSON.parse(JSON.stringify(response.data))

    //       if(response == []) // there are no favorite recipes for the specific user
    //       {
    //         return;
    //       }
    //       else
    //       {
    //         this.isEmpty = false;
    //         this.recipes = response
    //       }
          

    //     } catch (err)
    //     {
    //       console.log("got err")
    //       console.log(err.response);
    //     }
    //   },
    isEmptyFavorites()
    {
        console.log("fav_is_empty")
        console.log(this.isEmpty)
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