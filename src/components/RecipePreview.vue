<template>
  <div>

    
      <div :title="recipe.title" class="recipe-title">
        <b>
          {{ recipe.title }}
        </b>
      </div>

      <div>

        <router-link v-if="!isPrivate" :to="{ name: 'recipe', params: { recipeId: recipe.id } }" class="recipe-preview">
          <div class="recipe-body">
            <img v-if="image_load" :src="recipe.image" class="recipe-image" />
          </div>
        </router-link>

          <div align="center" v-if="isPrivate" class="recipe-body">
            <img v-if="image_load" :src="recipe.image" class="recipe-image" width="350" height="250" />



          </div>

      </div>

      <br>
      <br>
      <br>

      <div v-if="!isPrivate">
        <b-container>
          <b-row>
            <b-col id="recipeInfo">
              <li>{{ recipe.readyInMinutes }} minutes</li>
              <li>{{ recipe.aggregateLikes }} likes</li>
              <li  v-if = recipe.watched > watched: yes </li>
              <li  v-else> watched: no </li>
              <li v-if = recipe.favorite>favorite: yes</li>
              <li  v-else> favorite: no </li>
              <br><br><br><br>
            </b-col>
            

          <!-- check me! -->
            <b-col v-if = "!recipe.favorite && !isPrivate">
              <b-button @click="addToFavorites()" variant="outline-info" >{{this.button_message}}</b-button>
            </b-col>

            <b-col v-if = "recipe.favorite">
              <b-button variant="outline-info" disabled>Marked as favorite</b-button>
            </b-col>
            <!-- check me! -->

          </b-row>
        </b-container>
      </div>


    <div v-if="isPrivate">
            <b-container>
              <b-row>
                <b-col id="a">
                  <li>{{ recipe.readyInMinutes }} minutes</li>
                  <li>{{ recipe.aggregateLikes }} likes</li>
                  <li  v-if = recipe.watched > watched: yes </li>
                  <li  v-else> watched: no </li>
                  <li v-if = recipe.favorite>favorite: yes</li>
                  <li  v-else> favorite: no </li>
                  <br><br><br><br>
                </b-col>

                <b-col>
                 <li>instructions: {{ recipe.instructions }} </li>
                </b-col>

                <b-col>
                 <li> ingredients: {{ recipe.ingredients }} </li>
                </b-col>
                

              <!-- check me! -->
                <b-col v-if = "!recipe.favorite && !isPrivate">
                  <b-button @click="addToFavorites()" variant="outline-info" >{{this.button_message}}</b-button>
                </b-col>

                <b-col v-if = "recipe.favorite">
                  <b-button variant="outline-info" disabled>Marked as favorite</b-button>
                </b-col>
                <!-- check me! -->

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
  },
  data() {
    return {
      image_load: false,
      button_message: "Add to favorites",
    };
  },
  props: {
    recipe: {
      type: Object,
      required: true
    }, 
    isPrivate: {
      type: Boolean,
      required: true
    },
  },
    methods:{
      async addToFavorites()
      {

         try{
          let response = await this.axios.post(
            this.$root.store.server_domain + "/users/favorites",
            {
              recipeId : this.recipe["id"],
            }
          );

          if(response.data != "The recipe is already marked as favorite") // the recipe has been added to the user favorite recipes
          {
            this.recipe.favorite = true
            this.button_message = "Marked as favorites"
          }
        } 
        catch (err)
        {
          console.log("got err")
          console.log(err.response);
        }
      },
    }
  

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
