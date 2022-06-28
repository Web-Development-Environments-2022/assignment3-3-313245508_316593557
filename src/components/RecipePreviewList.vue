<template>
  <b-container>
    <h3>
      <!-- {{ title }} -->
      <slot></slot>
    </h3>
    <br>
    <br>
    <b-row>
      <b-col v-for="r in recipes" :key="r.id">
        <RecipePreview class="recipePreview" :recipe="r" />
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
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
    isEmpty: {
      type: Boolean
    }
    
  },
  data() {
    return {
      recipes: [],
    };
  },
  mounted() {
    if(this.id == "randomRecipeID")
    {
      this.updateRecipes();
    }
    else if (this.id == "lastWatchedRecipeID")
    {
      // console.log("hahahaha1")
      // this.lastWatchedRecipes();
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
    else if (this.id == "familyRecipeID")
    {
      this.showFamilyRecipes()
    }
    
  },
  methods: {
    async updateRecipes() {
      try {
        const response = await this.axios.get(
          this.$root.store.server_domain + "/home/", 
          // "https://test-for-3-2.herokuapp.com/recipes/random"
        );

        // console.log(response);
        const recipes = response.data;
        this.recipes = [];
        this.recipes.push(...recipes);
        // console.log(this.recipes);
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

        // console.log(response);
        const recipes = response.data;
        this.recipes = [];
        this.recipes.push(...recipes);
        // console.log(this.recipes);
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

          if(response.length == 0) // there are no family recipes for the specific user
          {
            // return;
          }
          else
          {
            console.log("response private")
            console.log(response)
            this.isEmpty = false;
            this.recipes = response
            this.$emit('isEmpty', this.isEmpty)
          }
        } catch (err)
        {
          console.log(err.response);
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
            // return;
          }
          else
          {
            
            this.isEmpty = false;
            this.recipes = response
            this.$emit('isEmpty', this.isEmpty)
          }
          

        } catch (err)
        {
          console.log("got err")
          console.log(err.response);
        }
      },

        async showFamilyRecipes()
      {
        try{
          let response = await this.axios.get(
            this.$root.store.server_domain + "/users/family",{
           
            }
          );
          console.log(response)
          if(response.data.length == 0) // there are no family recipes for the specific user
          {
            // return;
          }
          else
          {
            console.log("response family")
            
            const searchResults = response.data;
            console.log(searchResults)
            this.recipes = [];
            this.recipes.push(...searchResults);
            console.log(this.recipes)
            this.isEmpty = false;
            this.$emit('isEmpty', this.isEmpty)
          }
          

        } catch (err)
        {
          console.log("got err family")
          console.log(err.response);
        }
      },

      async showSearchedRecipes() 
      {
        try{

        } catch (error) {
          console.log(error);
        }
      }
  }
};
</script>

<style lang="scss" scoped>
.container {
  min-height: 400px;
}
</style>
