<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <router-link class="navbar-brand" to="/">BLOK</router-link>
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarSupportedContent"
      aria-controls="navbarSupportedContent"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav ml-auto">
        <li class="nav-item active">
          <router-link to="/" class="nav-link">
            Home
            <span class="sr-only">(current)</span>
          </router-link>
        </li>
        <li class="nav-item" v-if="!isLoggedIn">
          <router-link to="/login" class="nav-link">Login</router-link>
        </li>
        <li class="nav-item" v-if="isLoggedIn">
          <router-link to="/saved" class="nav-link">Saved Posts</router-link>
        </li>
        <li class="nav-item" v-if="isLoggedIn">
          <router-link to="/create" class="nav-link">Create Post</router-link>
        </li>
        <li class="nav-item" v-if="!isLoggedIn">
          <router-link to="/register" class="nav-link">Register</router-link>
        </li>
        <li class="nav-item" v-if="isLoggedIn">
          <router-link to="/myposts" class="nav-link">My Posts</router-link>
        </li>
        <li class="nav-item" v-if="isLoggedIn">
          <router-link to="/profile" class="nav-link">Profile</router-link>
        </li>
        <li class="nav-item" v-if="isLoggedIn">
          <a href="#" to="/logout" class="nav-link" @click.prevent="logoutUser"
            >Logout</a
          >
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
import { mapGetters } from "vuex";
import store from "../store";
import authServices from "../services/authServices";

export default {
  computed: {
    ...mapGetters(["isLoggedIn"]),
  },
  methods: {
    async logoutUser() {
      await authServices.logout();
      store.commit("logout");
      this.$router.push("/login");
    },
  },
};
</script>

<style></style>
