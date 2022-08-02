<template>
  <b-container v-if="isEmpty">
    <h3>
      <!-- {{ title }} -->
      <slot></slot>
    </h3>
    <br>
    <br>

    <!-- <div v-if="emptyFlag" >

    <b-row v-for="n in NumOfLists">
      <b-col v-for="r in recipes[0 + i,3 + i]" :key="r.id">
        <RecipePreview class="recipePreview" :recipe="r" />
      </b-col>
      <div v-if="updateIndex()"></div>
    </b-row>

    </div> -->


    <div v-if="emptyFlag" >

    <b-row>
      <b-col v-for="r in recipes" :key="r.id">
        <RecipePreview class="recipePreview" :recipe="r" />
      </b-col>
    </b-row>

    </div>


      <div v-if="!emptyFlag">
        <b>There are no Recipes to show..</b>
      </div>
  </b-container>

  <b-container v-else>
    <h2>There are no recipes to show</h2>
  </b-container>
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
<<<<<<< HEAD
      emptyFlag: true,
      NumOfLists: 0,
      i: 0,
=======
      isEmpty: true,
>>>>>>> b4f386a786884e3347814d8f794fe2aaaef95d86
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
        console.log(this.recipes)
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
          if(response.length == 0) // there are no private recipes for the specific user
          {
<<<<<<< HEAD
            this.emptyFlag = false;
            return;
          }
          else
          {
            this.recipes = response
            updateNumOfLists(response.length)
=======
            this.isEmpty = true
            // return;
          }
          else
          {
            console.log("response private")
            console.log(response)
            // this.isEmpty = false;
            this.recipes = response
            // this.$emit('isEmpty', this.isEmpty)
>>>>>>> b4f386a786884e3347814d8f794fe2aaaef95d86
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
          console.log("response favorite")
          console.log(response)
          if(response.length == 0) // there are no favorite recipes for the specific user
          {
<<<<<<< HEAD
           this.emptyFlag = false;
           return;
          }
          else
          {
            this.recipes = response
            updateNumOfLists(response.length)
=======
            this.isEmpty = true
            // return;
          }
          else
          {
            // this.isEmpty = false;
            this.recipes.push(...response);
            // this.recipes = response
            this.$emit('isEmpty', this.isEmpty)
>>>>>>> b4f386a786884e3347814d8f794fe2aaaef95d86
          }
        } 
        catch (err)
        {
<<<<<<< HEAD
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
=======
          console.log("got err")
          console.log(err);
>>>>>>> b4f386a786884e3347814d8f794fe2aaaef95d86
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

.container {
  min-height: 400px;
}
</style>
