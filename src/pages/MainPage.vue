<template>
  <div class="container">
    <br>
    <h1 class="title">Main Page</h1>
    <br>
    <br>
    <br>
    <RecipePreviewList title="Random Recipes" class="RandomRecipes center" />
    <br>
    <br>
    <br>
    <RecipePreviewList
      title="Last Viewed Recipes"
      :class="{
        RandomRecipes: true,
        blur: !$root.store.username,
        center: true
      }"
      disabled
    ></RecipePreviewList>
    <!-- <div
      style="position: absolute;top: 70%;left: 50%;transform: translate(-50%, -50%);"
    >
      Centeredasdasdad
    </div>-->
  </div>
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
  margin: 10px 0 10px;
  background-image: "https://media.istockphoto.com/photos/healthy-flat-lay-of-sliced-vegetables-composition-picture-id1198220441";

}
.title 
{
  text-align: center;
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
