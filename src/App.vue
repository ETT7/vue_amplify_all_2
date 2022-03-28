<template>
<authenticator>
  <template v-slot="{ user, signOut }">
    <h3>Current Login: {{ user.attributes.email }}</h3><button type="button" class="btn btn-outline-danger" @click="signOut">Signout</button>
    <div class="pos-f-t">
  <div class="collapse" id="navbarToggleExternalContent">
    <div class="bg-dark p-4">
      <router-link to="/uploadfiles" type="button" class="btn btn-secondary btn-lg btn-block">Upload</router-link><br><br>
    <router-link to="/users" type="button" class="btn btn-secondary btn-lg btn-block">Users</router-link><br><br>
    <router-link to="/tasks" type="button" class="btn btn-secondary btn-lg btn-block">Tasks</router-link><br><br>
    <router-link to="/" type="button" class="btn btn-secondary btn-lg btn-block">Home</router-link><br><br>
    
    </div>
  </div>
  <nav class="navbar navbar-dark bg-dark">
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarToggleExternalContent" aria-controls="navbarToggleExternalContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
  </nav>
</div>
  <nav>
    
  </nav>
  <router-view/>
      </template>
    </authenticator>
</template>
<script>
import { Authenticator } from "@aws-amplify/ui-vue";
export default {

  components: {
    Authenticator,
  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
