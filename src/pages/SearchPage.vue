
<template>
  <div>
    <p><b>Enter query:</b></p>
    <b-form-input v-model="query" placeholder="Search recipe"></b-form-input>
    <!-- <div class="mt-2">Value: {{ query }}</div> -->
    
    <br>
    <p><b>Select number of results:</b></p>
    <b-form-select v-model="num_of_result_display" :options="num_of_result"></b-form-select>
    
    <br>
    <p><b>Select Cuisine: (Hold ctrl to select multiple options)</b></p>
    <b-form-select v-model="cuisine_display" :options="cuisine" multiple :select-size="4"></b-form-select>
    <br>
    <div class="mt-3">Choosed cuisines: <strong>{{ cuisine_display }}</strong></div>
    
    <br>
    <p><b>Select Diet type: (Hold ctrl to select multiple options)</b></p>
    <b-form-select v-model="diet_display" :options="diet" multiple :select-size="4"></b-form-select>
    <br>
    <div class="mt-3">Choosed diet types: <strong>{{ diet_display }}</strong></div>


    <br>
    <p><b>Select Intolerances: (Hold ctrl to select multiple options)</b></p>
    <b-form-select v-model="intolerance_display" :options="intolerance" multiple :select-size="4"></b-form-select>
    <br>
    <div class="mt-3">Choosed intolerances: <strong>{{ intolerance_display }}</strong></div>
    <br>

    <br>
    <b-button variant="outline-primary" @click='Search'> Search </b-button>

    <div id="result_div">
    <RecipePreviewList id="searched_recipes" title="Searched Recipes" class="SearchRecipes center" />
    </div>
  </div>

  
</template>

<script>
import RecipePreviewList from "../components/RecipePreviewList";
  export default {
    components: {
    RecipePreviewList
  },
    data() {
      return {
        query: '', 

        num_of_result_display: [],
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
    methods:{
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


          console.log(response)
        } catch (err){
          console.log("got errorrr")
          console.log(err.response);
          this.form.submitError = err.response.data.message;
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