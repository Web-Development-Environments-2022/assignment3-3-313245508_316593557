<template>
  <b-container>
    <h3>
      {{ title }}
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
    title: {
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
    if(this.title == "Random Recipes")
    {
      this.updateRecipes();
    }
    else if (this.title == "Last Viewed Recipes")
    {
      // console.log("hahahaha1")
      // this.lastWatchedRecipes();
      this.getLastWached();
    }
    else if (this.title == "Private Recipes")
    {
      this.showPrivateRecipes()
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
            console.log("response")
            console.log(response)
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
