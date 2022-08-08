<template>
  <div>

    <div v-if="emptyFlag">
    <b-row >
      <b-col id="recipeInfo" v-for="r in recipes" :key="r.id">
        <RecipePreview class="recipePreview" :recipe="r" :isPrivate="p" /> 
      </b-col>
    </b-row>


    </div>


      <div v-if="!emptyFlag" align="center">
        <b>There are no recipes to show..</b>
      </div>
  </div>
</template>

<script>
import { async } from "q";
import RecipePreview from "./RecipePreview.vue";
export default {
  name: "RecipePreviewList",
  components: {
    RecipePreview
  },
  props: {
    id: {
      type: String,
      required: true
    },
    // isEmpty: {
    //   type: Boolean
    // }
    
  },
  data() {
    return {
      recipes: [],
      emptyFlag: true,
      NumOfLists: 0,
      i: 0,
      p: false
    };
  },
  mounted() {
    if(this.id == "randomRecipeID")
    {
      this.updateRecipes();
    }
    else if (this.id == "lastWatchedRecipeID")
    {
      this.getLastWached();
    }
    else if (this.id == "privateRecipeID")
    {
      this.showPrivateRecipes()
    }
    else if (this.id == "favoriteRecipeID")
    {
      this.showFavoriteRecipes()
    }

    
  },
  methods: {
    async updateRecipes() {
      try {
        const response = await this.axios.get(
          this.$root.store.server_domain + "/home/", 
          // "https://test-for-3-2.herokuapp.com/recipes/random"
        );

        const recipes = response.data;
        this.recipes = [];
        this.recipes.push(...recipes);
      } catch (error) {
        console.log(error);
      }
    },

    async getLastWached() {
      try {
        const response = await this.axios.get(
          this.$root.store.server_domain + "/users/lastwatched",{withCredentials: true}
          // "https://test-for-3-2.herokuapp.com/recipes/random"
        );

        const recipes = response.data;
        this.recipes = [];
        this.recipes.push(...recipes);
      } catch (error) {
        console.log(error);
      }
    },

    async showPrivateRecipes()
    {
        try{
          let response = await this.axios.get(
            this.$root.store.server_domain + "/users/private",{ withCredentials: true, credentials: "include" }
          );

          response = JSON.parse(JSON.stringify(response.data))
          if(response.length == 0) // there are no private recipes for the specific user
          {
            this.emptyFlag = false;
            return;
          }
          else
          {
            this.p = true;
            this.recipes = response
            console.log(this.recipes)
            updateNumOfLists(response.length)
          }
        } catch (err)
        {
          console.log(err);
        }
      },

      async showFavoriteRecipes()
      {
        try{
          let response = await this.axios.get(
            this.$root.store.server_domain + "/users/favorites",
          );
          response = JSON.parse(JSON.stringify(response.data))
          if(response.length == 0) // there are no favorite recipes for the specific user
          {
           this.emptyFlag = false;
           return;
          }
          else
          {
            this.recipes = response
            updateNumOfLists(response.length)
          }
        } 
        catch (err)
        {
          console.log(err.response);
        }
      },

        async showFamilyRecipes()
      {
        try{
           console.log("no favorites")

          let response = await this.axios.get(
            this.$root.store.server_domain + "/users/family",{
           
            }
          );
          if(response.data.length == 0) // there are no family recipes for the specific user
          {
           this.emptyFlag = false;
           return;
          }
          else
          {
            const searchResults = response.data;
            this.recipes = [];
            this.recipes.push(...searchResults);
            updateNumOfLists(response.length)
          }
        } 
        catch (err)
        {
          console.log(err.response);
        }
      },

      async showSearchedRecipes() 
      {
        try
        {

        } 
        catch (error) 
        {
          console.log(error);
        }
      }, 
        async updateNumOfLists(len)
      {
        if(len <= 3)
        {
          this.NumOfLists = 1
        }
        else
          {
            if(len % 3 == 0)
              this.NumOfLists = int(len / 3) 
            else
              this.NumOfLists = int(len / 3) + 1
          }
      },
        async updateIndex()
        {
          this.i += 3;
        }
  }
  
};
</script>

<style lang="scss" scoped>

.recipePreview{
  width: 600px;
  align-items: center;
}


#recipeInfo {
border-width:2px;
border-style:groove;
border-color:rgb(62, 89, 115);
border-radius: 12px;
margin: 10px;
}

.container {
  min-height: 400px;
}
</style>



