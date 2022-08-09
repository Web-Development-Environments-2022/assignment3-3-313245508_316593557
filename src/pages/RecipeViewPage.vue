<template>
  <div class="container">
    <div v-if="recipe">
    <br>
      <div class="recipe-header mt-3 mb-4" align="center">
        <h1><b>{{ recipe.title }}</b></h1>
        <br><br>
        <img :src="recipe.image" class="center" />
        <br>
      </div>
      <div id="recipeInfo3" class="recipe-body">
        <div class="wrapper">
          <div class="wrapped">
            <div class="mb-3">
              <div> <b>Ready in: </b> {{ recipe.readyInMinutes }} minutes</div>
              <br>
              <div><b>Likes: </b>{{ recipe.aggregateLikes }} likes</div>
            </div>
            <b>Ingredients:</b>
            <ul>
              <li
                v-for="(r, index) in recipe.extendedIngredients"
                :key="index + '_' + r.id"
              >
                {{ r.original }}
              </li>
            </ul>
          </div>
          <div class="wrapped">
            <b>Instructions:</b>
            <ol>
              <li v-for="s in recipe._instructions" :key="s.number">
                {{ s.step }}
              </li>
            </ol>
          </div>
        </div>
      </div>
      <!-- <pre>
      {{ $route.params }}
      {{ recipe }}
    </pre
      > -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      recipe: null
    };
  },
  async created() {
    try {
      let response;
      // response = this.$route.params.response;

      try {
        let recipeId = this.$route.params.recipeId
        let recipeIdString = recipeId.toString();
        response = await this.axios.get(
          // "https://test-for-3-2.herokuapp.com/recipes/info",
          this.$root.store.server_domain + "/recipes/" + recipeIdString, { withCredentials: true, credentials: "include" }

          // {
          //   params: { id: this.$route.params.recipeId }
          // }
        );

        // console.log("response.status", response.status);
        if (response.status !== 200) this.$router.replace("/NotFound");
      } catch (error) {
        console.log("error.response.status", error.response.status);
        this.$router.replace("/NotFound");
        return;
      }

      let {
        analyzedInstructions,
        //instructions,
        extendedIngredients,
        aggregateLikes,
        readyInMinutes,
        image,
        title,
        watched,
        favorite
      } = response.data;
      console.log(aggregateLikes)

      let _instructions = analyzedInstructions
        .map((fstep) => {
          fstep.steps[0].step = fstep.name + fstep.steps[0].step;
          return fstep.steps;
        })
        .reduce((a, b) => [...a, ...b], []);

      let _recipe = {
        // instructions,
        _instructions,
        // analyzedInstructions,
        extendedIngredients,
        aggregateLikes,
        readyInMinutes,
        image,
        title,
        watched,
        favorite
      };

      this.recipe = _recipe;
    } catch (error) {
      console.log(error);
    }
  }
};
</script>

<style scoped>
.wrapper {
  display: flex;
}
.wrapped {
  width: 50%;
}
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}

#recipeInfo3 {
border-width:2px;
border-style:groove;
border-color:rgb(62, 89, 115);
border-radius: 12px;
margin: 10px;
padding: 10px;
}

</style>
