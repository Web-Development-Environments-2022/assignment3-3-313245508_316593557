<template>
  <div>

      <div :title="recipe.name" class="recipe-title">
        <b>
          {{ recipe.name }}
        </b>
      </div>

      <div>
        <!-- <router-link :to="{ name: 'recipe', params: { recipeId: recipe.recipe_id } }" class="recipe-preview"> -->
          <div class="recipe-body" align="center">
            <img v-if="image_load" :src="recipe.image" class="recipe-image" width="350" height="250"/>
          </div>
        <!-- </router-link> -->
      </div>

      <br>
      <br>
      <br>

      <div>
        <b-container>
          <b-row>
            <b-col>
              <li><b><u>Recipe Inventor:</u></b> {{ recipe.recipe_inventor }}</li>
              <li><b><u>When to make it:</u></b> {{ recipe.when_to_make_it }}</li>
              <li><b><u>Ingredients:</u></b> {{ recipe.ingredients }}</li>
              <li><b><u>Instructions:</u></b> {{ recipe.instructions }}</li>
              
            </b-col>


          </b-row>
        </b-container>
      </div>

  </div>
</template>

<script>
export default {
  mounted() {
    this.axios.get(this.recipe.image, { withCredentials: false}).then((i) => {
      this.image_load = true;
    });
    console.log(this.recipe)
    console.log("ggggggggggggggggggggggggggg")
  },
  data() {
    return {
      image_load: false,
    };
  },
  props: {
    recipe: {
      type: Object,
      required: true
    }
  },

  

    // id: {
    //   type: Number,
    //   required: true
    // },
    // title: {
    //   type: String,
    //   required: true
    // },
    // readyInMinutes: {
    //   type: Number,
    //   required: true
    // },
    // image: {
    //   type: String,
    //   required: true
    // },
    // aggregateLikes: {
    //   type: Number,
    //   required: false,
    //   default() {
    //     return undefined;
    //   }
    // }
  };
</script>

<style scoped>
.recipe-preview {
  display: flex;
  width: 90%;
  height: 100%;
  position: relative;
  margin: 10px 10px;
}
.recipe-preview > .recipe-body {
  width: 100%;
  height: 200px;
  position: relative;
}

.recipe-preview .recipe-body .recipe-image {
  margin-left: auto;
  margin-right: auto;
  margin-top: auto;
  margin-bottom: auto;
  display:flex;
  width: 400px;
  height: 250px;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  background-size: cover;
}

.recipe-title {
  text-align: center;
}

.recipe-preview .recipe-footer {
  width: 100%;
  height: 50%;
  overflow: hidden;
}

.recipe-preview .recipe-footer .recipe-title {
  padding: 10px 10px;
  width: 100%;
  font-size: 12pt;
  text-align: left;
  white-space: nowrap;
  overflow: hidden;
  -o-text-overflow: ellipsis;
  text-overflow: ellipsis;
}

.recipe-preview .recipe-footer ul.recipe-overview {
  padding: 5px 10px;
  width: 100%;
  display: -webkit-box;
  display: -moz-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  box-flex: 1;
  -webkit-flex: 1 auto;
  -ms-flex: 1 auto;
  flex: 1 auto;
  table-layout: fixed;
  margin-bottom: 0px;
}

.recipe-preview .recipe-footer ul.recipe-overview li {
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  -ms-box-flex: 1;
  box-flex: 1;
  -webkit-flex-grow: 1;
  flex-grow: 1;
  width: 90px;
  display: table-cell;
  text-align: center;
}
</style>
