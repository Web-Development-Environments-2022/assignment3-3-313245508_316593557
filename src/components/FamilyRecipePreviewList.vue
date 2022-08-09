<template>
<div>
  <b-container v-if="!isEmpty">
    <h3>
      <!-- {{ title }} -->
      <slot></slot>
    </h3>
    <br>
    <br>
    <b-row>
      <b-col id="recipeInfoFamily" v-for="r in recipes" :key="r.id">
        <FamilyRecipePreview class="recipePreview" :recipe="r" />
      </b-col>
    </b-row>
        <br><br><br><br><br>
  </b-container>
  

  <div v-if="isEmpty" align="center">
    <b-container>
        <b>There are no recipes to show..</b>
    </b-container>
  </div>
</div>
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
          if(response.data.length == 0) // there are no family recipes for the specific user
          {
            this.isEmpty = true
            return;
          }
          else
          {
            const searchResults = response.data;
            console.log(searchResults)
            this.isEmpty = false;
            this.recipes = searchResults;
          }
          

        } catch (err)
        {
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

#recipeInfoFamily {
border-width:2px;
border-style:groove;
border-color:rgb(62, 89, 115);
border-radius: 12px;
margin: 10px;
padding: 10px;
}
</style>
