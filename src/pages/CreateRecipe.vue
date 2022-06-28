
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

     
      <b-form-group id="input-group-5" v-slot="{ ariaDescribedby }">
        <b-form-checkbox-group
          v-model="form.vegetarian"
          id="checkboxes-4"
          :aria-describedby="ariaDescribedby"
        >
          <b-form-checkbox value="vegetarian">Vegetarian</b-form-checkbox>
        </b-form-checkbox-group>

        <b-form-checkbox-group
          v-model="form.vegan"
          id="checkboxes-4"
          :aria-describedby="ariaDescribedby"
        >
          <b-form-checkbox value="vegan">Vegan</b-form-checkbox>
        </b-form-checkbox-group>

        <b-form-checkbox-group
          v-model="form.gluten_free"
          id="checkboxes-4"
          :aria-describedby="ariaDescribedby"
        >
          <b-form-checkbox value="gluten_free">Gluten Free</b-form-checkbox>
        </b-form-checkbox-group>

      </b-form-group>
      <br>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
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
          image: '',
          vegetarian: [],
          vegan:[],
          gluten_free:[]
        },
        show: true
      }
    },
    methods: {
      async onSubmit(event) {
        event.preventDefault()
        const new_recipe = this.form
        console.log(JSON.stringify(new_recipe))
        if ("vegetarian" in new_recipe)
        {
          new_recipe["vegetarian"] = 1
        }
        else
        {
          new_recipe["vegetarian"] = 0
        }
        if (!typeof new_recipe["vegan"] === undefined)
        {
          new_recipe['vegan'] = 1
        }
        else
        {
          new_recipe['vegan'] = 0
        }
        if (!typeof new_recipe["gluten_free"] == undefined)
        {
          new_recipe['gluten_free'] = 1
        }
        else
        {
          new_recipe['gluten_free'] = 0
        }
        console.log(JSON.stringify(new_recipe))
        

        const response = await this.axios.post(
          this.$root.store.server_domain + "/users/private",

          {
            name: new_recipe["recipe_name"],
            preparation_time: new_recipe["preparation_time"],
            amount_of_meals: new_recipe["amount_of_meals"],
            ingredients: new_recipe["ingredients"],
            instructions: new_recipe["instructions"],
            popularity: 0,
            vegan: new_recipe["vegan"],
            vegetarian: new_recipe["vegetarian"],
            gluten_free: new_recipe["gluten_free"]
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
        this.form.vegetarian = []
        this.form.vegan = []
        this.form.gluten_free = []
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }
</script>