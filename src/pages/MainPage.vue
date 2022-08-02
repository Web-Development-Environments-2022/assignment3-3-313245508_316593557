<template>
<div>
  <br>
  <h1 class="title"><b>Main Page</b></h1>
  <table align="center">
    <td width="50%" >
      <br>
      <div class="container">
        <br>
        <h3 ><b>Random Recipes</b></h3>
        <br>
        <RecipePreviewList title="Random Recipes" id="randomRecipeID" class="RandomRecipes center" />

      </div>

    </td>
    
    <td width="50%">
      <br>
      <div>
        <br>
        <h3 :class="{
        blur: !$root.store.username,
        center: true
      }"><b>Last Viewed Recipes</b></h3>
      <br>
        <RecipePreviewList
      title="Last Viewed Recipes"
      id="lastWatchedRecipeID"
      :class="{
        RandomRecipes: true,
        blur: !$root.store.username,
        center: true
      }"
      disabled
    ></RecipePreviewList>
      </div>

    </td>
  </table>
</div>
  <!-- <div class="container">
    <br>
    <h1 class="title"><b>Main Page</b></h1>
    <br>
    <br>
    <h3><b>Random Recipes</b></h3>
    <RecipePreviewList title="Random Recipes" id="randomRecipeID" class="RandomRecipes center" />
    <br>
    <br>
    <br>
    <h3 :class="{
        blur: !$root.store.username,
        center: true
      }"><b>Last Viewed Recipes</b></h3>
    <RecipePreviewList
      title="Last Viewed Recipes"
      id="lastWatchedRecipeID"
      :class="{
        RandomRecipes: true,
        blur: !$root.store.username,
        center: true
      }"
      disabled
    ></RecipePreviewList>

  </div> -->
</template>

<script>
import RecipePreviewList from "../components/RecipePreviewList";
export default {
  components: {
    RecipePreviewList
  }
};
</script>

<style lang="scss" scoped>
.RandomRecipes {
  // margin: 10px 0 10px;
  background-image: "https://media.istockphoto.com/photos/healthy-flat-lay-of-sliced-vegetables-composition-picture-id1198220441";

}
.title 
{
  align-content: center;
}
.blur {
  -webkit-filter: blur(5px); /* Safari 6.0 - 9.0 */
  filter: blur(2px);
}
::v-deep .blur .recipe-preview {
  pointer-events: none;
  cursor: default;
}
</style>
