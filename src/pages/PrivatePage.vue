
<template>
  <div>
  <b-container>
    <br>
      <h1 class="title">
        <b>
        Private Recipes:
        </b>
      </h1>

      <div class="family_recipes" v-if="isEmptyPrivate()">
        <RecipePreviewList @isEmpty="doSomething" class="RandomRecipes center" />
      </div>

      <b-container v-if="isEmptyPrivate()">
        <h3 class="title">
          There are no private recipes
        </h3>
      </b-container>
  </b-container>
  </div>
  
</template>

<script>
// import RecipePreview from "../components/RecipePreview";
import RecipePreviewList from "../components/RecipePreviewList";


  export default {
    name: "private",
    components: {
      // RecipePreview,
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
    // this.showPrivateRecipes();  
    // },
    methods:
    {
    //   async showPrivateRecipes()
    // {
    //     try{
    //       let response = await this.axios.get(
    //         this.$root.store.server_domain + "/users/private",{ withCredentials: true, credentials: "include" }
    //       );

    //       response = JSON.parse(JSON.stringify(response.data))

    //       if(response == []) // there are no family recipes for the specific user
    //       {
    //         return;
    //       }
    //       else
    //       {
    //         console.log("gereerererere")
    //         this.isEmpty = false;
    //         this.recipes = response
    //       }
          

    //     } catch (err)
    //     {
    //       console.log("got err")
    //       console.log(err.response);
    //     }
    //   },
        isEmptyPrivate()
    {
        return this.isEmpty;
    },
    async doSomething(data)
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
