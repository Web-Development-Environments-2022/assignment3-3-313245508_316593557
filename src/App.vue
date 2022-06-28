<template>
  <div id="app">

    <div>
      <b-navbar type="dark" variant="dark">
        <b-navbar-nav>
          <b-nav-item to="/">Main page</b-nav-item>
          <b-nav-item to="/search">Search</b-nav-item>

        <span v-if="!$root.store.username">
          <b-nav-item to="/register">Register</b-nav-item>
        </span>

        <span v-else>

          <b-nav-item-dropdown text="Personal" down>
            <b-dropdown-item to="/users/private">Private</b-dropdown-item>
            <b-dropdown-item to="/users/favorites">Favorite</b-dropdown-item>
            <b-dropdown-item to="/users/family">Family</b-dropdown-item>
            <b-dropdown-item to="/users/createRecipe">Create Recipe</b-dropdown-item>
          </b-nav-item-dropdown>
          
        </span>

        <span v-if="!$root.store.username">
          <b-nav-item id="abc" to="/login">Login</b-nav-item>
        </span>

        <span v-else>
          <b-nav-item @click="Logout">Logout</b-nav-item>

      </span>
        </b-navbar-nav>
      </b-navbar>
    </div>

<!-- 
    <div id="nav">
      <router-link :to="{ name: 'main' }">Main page</router-link>|
      <router-link :to="{ name: 'search' }">Search</router-link>|
      <span v-if="!$root.store.username">
        <router-link :to="{ name: 'register' }">Register</router-link>|
        <router-link :to="{ name: 'login' }">Login</router-link>|
        
      </span>
      <span v-else>
        {{ $root.store.username }}: <button @click="Logout">Logout</button>| 
        <router-link :to="{ name: 'createRecipe' }">Create recipe</router-link>| 
        <router-link :to="{ name: 'favorites' }">Favorite</router-link>|
        <router-link :to="{ name: 'private' }">Private</router-link>|
        <router-link :to="{ name: 'family' }">Family</router-link>|
      </span>

      

    </div> -->
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",
  methods: {
    async Logout() {

      const response = await this.axios.post(
          this.$root.store.server_domain +"/Logout"
        );
      this.$root.store.logout();
      this.$root.toast("Logout", "User logged out successfully", "success");

      this.$router.push("/").catch(() => {
        this.$forceUpdate();
      });
    }
  }
};
</script>

<style lang="scss">
@import "@/scss/form-style.scss";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>



<!-- 
notes:
1. change layout of recipes (search/personal pages)
2. create recipe -> modal
3. favorite button
3. family recipe preview/list compenent
4. last recipes watched in the main page
5. validations
6. design
7. Real Server..
8. change yamel
-->
