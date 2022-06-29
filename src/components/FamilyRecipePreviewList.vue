<template>
  <b-container v-if="isEmpty">
    <h3>
      <!-- {{ title }} -->
      <slot></slot>
    </h3>
    <br>
    <br>
    <b-row>
      <b-col v-for="r in recipes" :key="r.id">
        <FamilyRecipePreview class="recipePreview" :recipe="r" />
      </b-col>
    </b-row>
  </b-container>

  <b-container v-else>
    <h2>There are no recipes to show</h2>
  </b-container>
</template>

<script>
import FamilyRecipePreview from "./FamilyRecipePreview.vue";
export default {
  name: "familyrecipepreviewlist",
  components: {
    FamilyRecipePreview
},
  props: {
    id: {
      type: String,
      required: true
    },

    
  },
  data() {
    return {
      recipes: [],
      isEmpty: true,
    };
  },
  mounted() {
      this.showFamilyRecipes()
    
  },
  methods: {
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
            this.isEmpty = true
            // return;
          }
          else
          {
            console.log("response family")
            
            const searchResults = response.data;
            // this.recipes = [];
            this.recipes = searchResults;
          }
          

        } catch (err)
        {
          console.log("got err family")
          console.log(err);
        }
      },

     
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
