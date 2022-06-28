
<template class="aaa">
      <div>
  <b-container>
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


      <div class="favorite_recipes">
        <div class="favorite_recipes" v-for="r in recipes" :key="r.id">
            <RecipePreview class="recipePreview" :recipe="r" />
        </div>
      </div>

        <b-container v-if="isEmptyFavorites()">
      <h3 class = "title">
        There are no favorite recipes
      </h3>
        </b-container>
    </b-container>
  </div>

  
</template>

<script>
import RecipePreview from "../components/RecipePreview";

  export default {
    name: "favorites",
    components: {
      RecipePreview
    },
    data() {
      return {
        recipes: [], 
        isEmpty: true,
      }
    },
    mounted() 
    {
    this.showFavoriteRecipes();  
    },
    methods:{
      async showFavoriteRecipes()
    {
        try{
          let response = await this.axios.get(
            this.$root.store.server_domain + "/users/favorites",
          );

          response = JSON.parse(JSON.stringify(response.data))

          if(response == []) // there are no favorite recipes for the specific user
          {
            return;
          }
          else
          {
            this.isEmpty = false;
            this.recipes = response
          }
          

        } catch (err)
        {
          console.log("got err")
          console.log(err.response);
        }
      },
          isEmptyFavorites()
    {
        return this.isEmpty;
    },
    }, 
  }
  
</script>


<style>

.title 
{
  text-align: center;
}

</style>