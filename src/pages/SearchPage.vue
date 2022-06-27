import Multiselect from 'vue-multiselect'


<template>

  <div>
    <b-form-input v-model="text" placeholder="Search Recipe"></b-form-input>
    <!-- <div class="mt-2">Value: {{ text }}</div> -->
    <div>

      <div>
  <label class="typo__label">Simple select / dropdown</label>
  <multiselect v-model="value" :options="options" :multiple="true" :close-on-select="false" :clear-on-select="false" :preserve-search="true" placeholder="Pick some" label="name" track-by="name" :preselect-first="true">
    <template slot="selection" slot-scope="{ values, search, isOpen }"><span class="multiselect__single" v-if="values.length &amp;&amp; !isOpen">{{ values.length }} options selected</span></template>
  </multiselect>
  <pre class="language-json"><code>{{ value  }}</code></pre>
</div>






    <!-- <b-form-select v-model="Cuisine" :options="Cuisine"></b-form-select>
    <b-form-select v-model="number_of_results" :options="number_of_results"></b-form-select>
    <b-form-select v-model="diet_type" :options="diet_type"></b-form-select>
    <b-form-select v-model="intolerances" :options="intolerances"></b-form-select> -->


  <!-- <b-dropdown id="Cuisine" text="Cuisine" class="m-md-2">
    <b-dropdown-item>African</b-dropdown-item>
    <b-dropdown-item>American</b-dropdown-item>
    <b-dropdown-item>British</b-dropdown-item>
    <b-dropdown-item>Cajun</b-dropdown-item>
    <b-dropdown-item>Caribbean</b-dropdown-item>
    <b-dropdown-item>Chinese</b-dropdown-item>
    <b-dropdown-item>Eastern European</b-dropdown-item>
    <b-dropdown-item>European</b-dropdown-item>
    <b-dropdown-item>French</b-dropdown-item>
    <b-dropdown-item>German</b-dropdown-item>
    <b-dropdown-item>Greek</b-dropdown-item>
    <b-dropdown-item>Indian</b-dropdown-item>
    <b-dropdown-item>Irish</b-dropdown-item>
    <b-dropdown-item>Italian</b-dropdown-item>
    <b-dropdown-item>Japanese</b-dropdown-item>
    <b-dropdown-item>Jewish</b-dropdown-item>
    <b-dropdown-item>Korean</b-dropdown-item>
    <b-dropdown-item>Latin American</b-dropdown-item>
    <b-dropdown-item>Mediterranean</b-dropdown-item>
    <b-dropdown-item>Mexican</b-dropdown-item>
    <b-dropdown-item>Middle Eastern</b-dropdown-item>
    <b-dropdown-item>Nordic</b-dropdown-item>
    <b-dropdown-item>Southern</b-dropdown-item>
    <b-dropdown-item>Spanish</b-dropdown-item>
    <b-dropdown-item>Thai</b-dropdown-item>
    <b-dropdown-item>Vietnamese</b-dropdown-item>
  </b-dropdown>

  <b-dropdown id="number_of_results" text="Number of results" class="m-md-2">
    <b-dropdown-item>5</b-dropdown-item>
    <b-dropdown-item>10</b-dropdown-item>
    <b-dropdown-item>15</b-dropdown-item>
  </b-dropdown>

<b-dropdown id="diet_type" text="Diet type" class="m-md-2">
    <b-dropdown-item>Gluten Free</b-dropdown-item>
    <b-dropdown-item>Ketogenic</b-dropdown-item>
    <b-dropdown-item>Vegeterian </b-dropdown-item>
    <b-dropdown-item>Lacto-Vegetarian</b-dropdown-item>
    <b-dropdown-item>Ovo-Vegetarian</b-dropdown-item>
    <b-dropdown-item>Vegan</b-dropdown-item>
    <b-dropdown-item>Pescetarian</b-dropdown-item>
    <b-dropdown-item>Paleo</b-dropdown-item>
    <b-dropdown-item>Primal</b-dropdown-item>
    <b-dropdown-item>Low FODMAP</b-dropdown-item>
    <b-dropdown-item>Whole30</b-dropdown-item>
  </b-dropdown>


<b-dropdown id="intolerances" text="Intolerances" class="m-md-2">
    <b-dropdown-item>Dairy</b-dropdown-item>
    <b-dropdown-item>Egg</b-dropdown-item>
    <b-dropdown-item>Gluten </b-dropdown-item>
    <b-dropdown-item>Grain</b-dropdown-item>
    <b-dropdown-item>Peanut</b-dropdown-item>
    <b-dropdown-item>Seafood</b-dropdown-item>
    <b-dropdown-item>Sesame</b-dropdown-item>
    <b-dropdown-item>Shellfish</b-dropdown-item>
    <b-dropdown-item>Soy</b-dropdown-item>
    <b-dropdown-item>Sulfite</b-dropdown-item>
    <b-dropdown-item>Tree Nut</b-dropdown-item>
    <b-dropdown-item>Wheat</b-dropdown-item>
  </b-dropdown> -->

  <b-button variant="primary">Search</b-button>


</div>

  </div>
</template>




<script src="https://unpkg.com/vue-multiselect@2.1.0">

<link rel="stylesheet" href="https://unpkg.com/vue-multiselect@2.1.0/dist/vue-multiselect.min.css">

  export default {
    data() {
    return {
      value: [],
      options: [
        { name: 'Vue.js', language: 'JavaScript' },
        { name: 'Adonis', language: 'JavaScript' },
        { name: 'Rails', language: 'Ruby' },
        { name: 'Sinatra', language: 'Ruby' },
        { name: 'Laravel', language: 'PHP' },
        { name: 'Phoenix', language: 'Elixir' }
      ]
    }
  }
}

</script>