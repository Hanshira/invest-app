<template>

<b-navbar class="navbar-class" toggleable="sm" type="dark" variant="dark">

  

  <b-navbar-brand>
      <router-link v-if="!$root.user" class="navbar-item" to="/">
      <img type="dark" src="/pictures/icon.png" height="45">
    </router-link>
    <router-link v-if="$root.user" class="navbar-item" to="/searchNew">
      <img type="dark" src="/pictures/icon.png" height="45">
    </router-link>
  </b-navbar-brand>
  <b-navbar-nav>
  <b-nav-item v-if="$root.user" to="/dashboard" >Dashboard</b-nav-item>
  <b-nav-item v-if="$root.user" to="/searchNew"  @click.native="isActive = false">Search</b-nav-item>
  </b-navbar-nav>

<b-navbar-toggle target="nav_collapse"></b-navbar-toggle>
  <b-collapse is-nav id="nav_collapse">

  

    <!-- Right aligned nav items -->

<!-- if not logged in -->
     <b-navbar-nav class="ml-auto" v-if="!$root.user">
    <b-button  variant='outline-secondary' to="/login"  @click.native="isActive = false">Login</b-button>
    </b-navbar-nav>

<!-- if logged in -->
    <b-navbar-nav class="ml-auto " v-else>

      <b-nav-item-dropdown id="ddown-right" right text="Right align">
      <template slot="button-content">
        <em> 
          <div  v-if="!$root.user.picture" class="icon-image">
            <b-img  height="50" rounded src="/pictures/person.png" fluid/>
          </div>
          <div  v-if="$root.user.picture" class="icon-image" >
            <b-img  rounded :src="$root.user.picture" fluid/>
          </div>
        </em>
      </template>
        <b-dropdown-item to="/profile"  @click.native="isActive = false">My profile</b-dropdown-item>
        <b-dropdown-item to="/edit"  @click.native="isActive = false">Edit my profile</b-dropdown-item>
        <b-dropdown-divider></b-dropdown-divider>
        <b-dropdown-item to="/wishlist"  @click.native="isActive = false">My wishlist</b-dropdown-item>
        <b-dropdown-divider></b-dropdown-divider>
        <b-dropdown-item to="/login" @click="logout">Logout</b-dropdown-item>
      </b-nav-item-dropdown>
  
    </b-navbar-nav>  

  </b-collapse>
</b-navbar>



</template>


<script>
import { logout } from "../api";

export default {
  data() {
    return {
      isActive: false
    };
  },

  methods: {
    logout() {
      logout();
      this.$root.user = null;
      this.$router.push("/login");
    }
  }
};
</script>

<style>
.icon-image {
  margin-top: -5px;
  margin-right: 5px;
  float: left;
  width: 30px;
  height: 30px;
}

.navbar-class {
  background-color: transparent;
}
</style>


