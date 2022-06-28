
<template>
  <div>
  <b-container>
      <h3>
         <b>
        Family Recipes:
        </b>
      </h3>

      <div class="family_recipes">
        <div class="family_recipes" v-for="r in recipes" :key="r.id">
            <RecipePreview class="recipePreview" :recipe="r" />
        </div>
      </div>

        <b-container v-if="isEmptyFamily()">
      <h3>
        There are no family recipes
      </h3>
        </b-container>
    </b-container>

  </div>

  
</template>

<script>
import RecipePreview from "../components/RecipePreview";

  export default {
    name: "family",
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
    this.showFamilyRecipes();  
    },
    methods:
    {
      async showFamilyRecipes()
    {
        try{
          let response = await this.axios.get(
            this.$root.store.server_domain + "/users/family",{
              params: 
              {

              }
            }
          );
          if(response == []) // there are no family recipes for the specific user
          {
            return;
          }
          else
          {
            isEmpty = false;
            const searchResults = response.data;
            this.recipes = [];
            this.recipes.push(...searchResults);
          }
          

        } catch (err)
        {
          console.log("got err")
          console.log(err.response);
        }
      },
          isEmptyFamily()
    {
        return this.isEmpty;
    },

    }, 
  }
  
</script>