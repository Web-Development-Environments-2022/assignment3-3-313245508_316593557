<template>
  <div>
    <h1>Create your private Recipe:</h1>
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <b-form-group
        id="input-group-1"
        label="Recipe name:"
        label-cols-sm="3"
        label-for="input-1"
      >
        <b-form-input
          id="input-1"
          v-model="form.recipe_name"
          placeholder="Enter recipe name"
          required
        ></b-form-input>
      </b-form-group>
      <br>

      <b-form-group id="input-group-2" label="Preparation time:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.preparation_time"
          placeholder="Enter preparation time"
          required
        ></b-form-input>
      </b-form-group>
      <br>

      <b-form-group id="input-group-3" label="Amount of meals:" label-for="input-3">
        <b-form-input
          id="input-3"
          v-model="form.amount_of_meals"
          placeholder="Enter amount of meals"
          required
        ></b-form-input>
      </b-form-group>
      <br>

      <b-form-group id="input-group-4" label="Image URL:" label-for="input-4">
        <b-form-input
          id="input-4"
          v-model="form.image"
          placeholder="Enter image URL"
          required
        ></b-form-input>
      </b-form-group>
      <br>

      <b-form-group
        id="input-group-ingredients"
        label-cols-sm="3"
        label="Ingredients:"
        label-for="ingredients"
      >
        <b-form-textarea 
          class="form-control" 
          id="ingredients" 
          rows="3"
          placeholder="Enter ingredients"
          v-model="form.ingredients"
          required
        ></b-form-textarea>
      </b-form-group>
      <br>

      <b-form-group
        id="input-group-instructions"
        label-cols-sm="3"
        label="Instructions:"
        label-for="instructions"
      >
        <b-form-textarea 
          class="form-control" 
          id="instructions" 
          rows="3"
          placeholder="Enter instructions"
          v-model="form.instructions"
          required
        ></b-form-textarea>
      </b-form-group>
      <br>

     
      <b-form-group id="input-group-5">

        <b-form-checkbox v-model='vegetarian' uncheckd-value="0" value="1">Vegetarian</b-form-checkbox>
        <b-form-checkbox v-model='vegan' uncheckd-value="0" value="1">Vegan</b-form-checkbox>
        <b-form-checkbox v-model='gluten_free' uncheckd-value="0" value="1">Gluten Free</b-form-checkbox>

      </b-form-group>
      <br>
      <table align="center">
        <td>
          <b-button type="submit" variant="primary">Submit</b-button>
        </td>
        <td>

        </td>
        <td>
          
        </td>
        <td>

        </td>
        <td>
      <b-button type="reset">Reset</b-button>
        </td>

      </table>
    </b-form>
   
  </div>
</template>

<script>
  export default {
    data() {
      return {
        form: {
          recipe_name: '',
          preparation_time: '',
          amount_of_meals: '',
          ingredients: '',
          instructions: '',
          image: ''
        },
        vegetarian: '0',
        vegan:'0',
        gluten_free:'0',
        show: true
      }
    },
    methods: {
      async onSubmit(event) {
        event.preventDefault()
        const new_recipe = this.form

        const response = await this.axios.post(
          this.$root.store.server_domain + "/users/private",

          {
            name: new_recipe["recipe_name"],
            preparation_time: new_recipe["preparation_time"],
            amount_of_meals: new_recipe["amount_of_meals"],
            ingredients: new_recipe["ingredients"],
            instructions: new_recipe["instructions"],
            image: new_recipe['image'],
            popularity: 0,
            vegan: this.vegan,
            vegetarian: this.vegetarian,
            gluten_free: this.gluten_free
          }
        )

        console.log(response)

      },
      onReset(event) {
        event.preventDefault()
        // Reset our form values
        this.form.recipe_name = ''
        this.form.preparation_time = ''
        this.form.amount_of_meals = ''
        this.form.ingredients = ''
        this.form.instructions = ''
        this.form.image = ''
        this.form.vegetarian = ''
        this.form.vegan = ''
        this.form.gluten_free = ''
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }
</script>