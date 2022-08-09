
<template>
  <div>
    <div :style="{
        'background-image': `url(https://media.istockphoto.com/photos/healthy-flat-lay-of-sliced-vegetables-composition-picture-id1198220441?k=20&m=1198220441&s=612x612&w=0&h=u9Z7_jok37dMOl41oRovtsIyUk_yWDwH_pADOOwSalg=)`,}">
        <br>
        <br>
    <br>
    <h1 class = "title"><b>Search Recipes</b></h1>
    <br>
    <br>



    <br>

  </div>

    <b-form-input v-if="HavePastSearches()" v-model="query" placeholder="Search recipe"></b-form-input>
    <b-form-input v-else v-model="query" :placeholder="lastSearchedQuery"></b-form-input>

    
    <br>
      <b-container>
        ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
        <br><br>
        <b-row>
          <b-col>
        <p><b>Select number of results:</b></p>
          </b-col>
          <b-col class = "title">
        <b-form-select v-model="num_of_result_display" :options="num_of_result"></b-form-select>
          </b-col>
        </b-row>
        ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
        <br>
        <br>

        <b-row>
          <b-col>
        <p><b>Select Cuisine: (Hold ctrl to select/deselect multiple options)</b></p>
          </b-col>
          <b-col class = "title">
        <b-form-select v-model="cuisine_display" :options="cuisine" multiple :select-size="4"></b-form-select>
          </b-col>
        </b-row>
        <b-row>
                  <div class="mt-3">Choosed cuisines: <strong>{{ cuisine_display }}</strong></div>
        </b-row>
        ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

        <br>
        <br>

        <b-row>
          <b-col>
        <p><b>Select Diet type: (Hold ctrl to select/deselect multiple options)</b></p>
          </b-col>
          <b-col class = "title">
        <b-form-select v-model="diet_display" :options="diet" multiple :select-size="4"></b-form-select>
          </b-col>
        </b-row>
        <b-row>
        <div class="mt-3">Choosed diet types: <strong>{{ diet_display }}</strong></div>
        </b-row>
        ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
        <br>
        <br>
        <b-row>
          <b-col>
        <p><b>Select Intolerances: (Hold ctrl to select/deselect multiple options)</b></p>
          </b-col>
          <b-col class = "title">
        <b-form-select v-model="intolerance_display" :options="intolerance" multiple :select-size="4"></b-form-select>
          </b-col>
        </b-row>
        <b-row>
        <div class="mt-3">Choosed intolerances: <strong>{{ intolerance_display }}</strong></div>
        </b-row>
        ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    </b-container>
    <br>
    <br>
    <div class = "title">
    <b-button class = "title" variant="outline-primary" @click='Search'> Search </b-button>
    
    </div>
        <br>
        <br>


  <div v-if="showResults">

  <b-container v-if="isEmpty()">
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  <br><br><br>
      <h3 align="center">
        <b>
        Search Results
        </b>
      </h3>

      <div >
        <div v-for="r in recipes" :key="r.id">
        <br><br>
            <RecipePreview id="recipeInfo2" class="recipePreview" :recipe="r" />
        </div>
      </div>
  </b-container>


  <b-container v-if="!isEmpty()" align="center">
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  <br><br>
      <h3>
        <b>
        There are no search results..
        </b>
      </h3>
      <br>
  </b-container>

    </div>

  </div>

  
</template>

<script>
// import RecipePreviewList from "../components/RecipePreviewList";
import RecipePreview from "../components/RecipePreview";

  export default {
    name: "searchResult",
    components: {
      RecipePreview
    },
    data() {
      return {
        recipes: [],
        lastSearched: false,
        showResults: false,
        lastSearchedQuery: "",
        query: '',
        num_of_result_display: 5,
        num_of_result: [
          { value: '5', text: '5' },
          { value: '10', text: '10' },
          { value: '15', text: '15' }
        ],

        cuisine_display: [],
        cuisine: [
          { value: 'African', text: 'African' },
          { value: 'American', text: 'American' },
          { value: 'Cajun', text: 'Cajun' },
          { value: 'Caribbean', text: 'Caribbean' },
          { value: 'Chinese', text: 'Chinese' },
          { value: 'Eastern European', text: 'Eastern European' },
          { value: 'European', text: 'European' },
          { value: 'French', text: 'French' },
          { value: 'German', text: 'German' },
          { value: 'Greek', text: 'Greek' },
          { value: 'Indian', text: 'Indian' },
          { value: 'Italian', text: 'Italian' },
          { value: 'Japanese', text: 'Japanese' },
          { value: 'Jewish', text: 'Jewish' },
          { value: 'Korean', text: 'Korean' },
          { value: 'Latin American', text: 'Latin American' },
          { value: 'Mediterranean', text: 'Mediterranean' },
          { value: 'Mexican', text: 'Mexican' },
          { value: 'Middle Eastern', text: 'Middle Eastern' },
          { value: 'Nordic', text: 'Nordic' },
          { value: 'Southern', text: 'Southern' },
          { value: 'Spanish', text: 'Spanish' },
          { value: 'Thai', text: 'Thai' },
          { value: 'Vietnamese', text: 'Vietnamese' }
        ],

        diet_display: [],
        diet: [
          { value: 'Gluten Free', text: 'Gluten Free' },
          { value: 'Ketogenic', text: 'Ketogenic' },
          { value: 'Vegeterian', text: 'Vegeterian' },
          { value: 'Lacto-Vegetarian', text: 'Lacto-Vegetarian' },
          { value: 'Ovo-Vegetarian', text: 'Ovo-Vegetarian' },
          { value: 'Vegan', text: 'Vegan' },
          { value: 'Pescetarian', text: 'Pescetarian' },
          { value: 'Paleo', text: 'Paleo' },
          { value: 'Primal', text: 'Primal' },
          { value: 'Low FODMAP', text: 'Low FODMAP' },
          { value: 'Whole30', text: 'Whole30' }
          ],
        
        intolerance_display: [],
        intolerance: [
          { value: 'Dairy', text: 'Dairy' },
          { value: 'Egg', text: 'Egg' },
          { value: 'Gluten', text: 'Gluten' },
          { value: 'Grain', text: 'Grain' },
          { value: 'Peanut', text: 'Peanut' },
          { value: 'Seafood', text: 'Seafood' },
          { value: 'Sesame', text: 'Sesame' },
          { value: 'Shellfish', text: 'Shellfish' },
          { value: 'Soy', text: 'Soy' },
          { value: 'Sulfite', text: 'Sulfite' },
          { value: 'Tree Nut', text: 'Tree Nut' },
          { value: 'Wheat', text: 'Wheat' }
        ],
        
      }
    },
    mounted()
    {
      this.updateLastSearched();
    },
    methods:
    {
      HavePastSearches()
      {
        console.log("flag")
        console.log(this.lastSearched)
        return !this.lastSearched;
      },
      async updateLastSearched()
      {
        try{
          let response = await this.axios.get(
            this.$root.store.server_domain + "/users/lastSearched", 
          );
          if(response.data[0] == null) // there are no favorite recipes for the specific user
          {
            return;
          }
          else
          {
            this.lastSearched = true;
            this.lastSearchedQuery = "Last Searched: " + response.data[0]
          }
          

        } catch (err)
        {
          console.log("got err")
          console.log(err.response);
        }
      },
      isEmpty(){
        if(this.recipes.length > 0)
        {
          return true
        }
        else
        {
          return false
        }
    },

      async Search(){
        try{
          let cuisine_param = this.joinList(this.cuisine_display)
          let diet_param =  this.joinList(this.diet_display)
          let intolerance_param =  this.joinList(this.intolerance_display)
          let response = await this.axios.get(
            this.$root.store.server_domain + "/recipes/search",{
              params: {
              query : this.query,
              number: this.num_of_result_display,
              cuisine: cuisine_param, 
              diet: diet_param,
              intolerances: intolerance_param
              }
            }
          );

          const searchResults = response.data;
          this.recipes = [];
          this.recipes.push(...searchResults);
          this.showResults = true;



        } catch (err){
          console.log("got errorrr")
          console.log(err.response);
          // this.form.submitError = err.response.data.message;
          }
      },

      // Helper function that receives an object of array and returns a string of the elements comma separated
       joinList(object)
      {    
        let result_str = '';
        let list_of_object = JSON.parse(JSON.stringify(object))
        for(let index in Object.values(list_of_object)){
          result_str += list_of_object[index] + ","
        }
        result_str = result_str.slice(0, -1)
        
        return result_str
      }
    }
  }
</script>


<style>


.title 
{
  text-align: center;
  align-items: center;
}


#recipeInfo2 {
border-width:2px;
border-style:groove;
border-color:rgb(62, 89, 115);
border-radius: 12px;
margin: 10px;
padding: 10px;
}


</style>


