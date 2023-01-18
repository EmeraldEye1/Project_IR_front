<template>
  <div class="bg">
    <a href="/"><img class="logo" src="@/assets/s.jpg" alt="a" /></a>
    <div class="menu">
      <div class="navbar">
        <router-link class="ribbon" :to="{ name: 'home' }">Home</router-link>
        <router-link class="ribbon2" :to="{ name: 'about' }"
          >Bookmark</router-link
        >
      </div>

      <Form @submit="search" :validation-schema="schema">
        <Field name="search" type="text" class="form-control searchbar" />
        <div class="form-group">
          <button class="btn btn-primary btn-block search">
            <span>Search</span>
          </button>
        </div>
      </Form>
      <div id="nav">
        <nav class="navbar navbar-expand">
          <ul v-if="!GStore.currentUser" class="navbar-nav ml-auto">
            <li class="nav-item">
              <router-link to="/login" class="nav-link logout2">
                <font-awesome-icon icon="sign-in-alt" /> Login
              </router-link>
            </li>
          </ul>
          <ul v-if="GStore.currentUser" class="navbar-nav ml-auto logout">
            <li class="nav-item">
              <router-link to="/profile" class="nav-link">
                <font-awesome-icon icon="user" />
                {{ GStore.currentUser.name }}
              </router-link>
            </li>
            <p class="user">
              {{ GStore.currentUser.username }}
            </p>
            <li class="nav-item">
              <a class="nav-link" @click="logout">
                <font-awesome-icon icon="sign-out-alt" /> | Logout
              </a>
            </li>
          </ul>
        </nav>
      </div>
    </div>
  </div>
</template>
<script>
import { Form, Field } from 'vee-validate';
import AuthService from '../service/AuthService.js';
import AnimeService from '../service/anime/AnimeService.js';

export default {
  inject: ['GStore'],
  name: 'NavbarCom',
  components: {
    Form,
    Field
  },
  methods: {
    logout() {
      AuthService.logout();
      this.$router.go();
    },
    search(query) {
      console.log(query);
      AnimeService.searchAnime(query);
      // setTimeout(() => this.$route.push('animeList'), 200)
    }
  }
};
</script>
<style scoped>
/* #nav {
  position: cover;
  top: 1px;
  height: 60px;
  width: 1460px;
  background: rgba(146, 246, 149, 0.925);
  margin-right: 0.5rem;
  border-radius: 8px;
} */
.menu {
  display: flex;
  flex-direction: row;
}
MDBNavbar {
  display: flex;
  flex-direction: row;
}
/* .r {
  top: 20%;
  left: 40%;
  margin-left: -250px;
} */
* {
  margin: 0;
  padding: 0;
}
.logo {
  position: fixed;
  margin: -10px 0px 0px 480px;
  top: 10px;
  height: 60px;
  padding: 0 0px;
  width: 70px;
  border-radius: 8px;
  border-color: #0088ff;
}
.bg {
  top: 1px;
  position: fixed;
  background-color: #71f881;
  height: 60px;
  width: 1490px;
  margin-right: 0.5rem;
  border-radius: 8px;
}
.body {
  position: fixed;
  background-color: #ccd3d8;
  height: 100px;
  font-family: 'Raleway', sans-serif;
}
.ribbon {
  position: fixed;
  margin: 0px 0px 0px 430px;
  background-color: rgb(83, 143, 27);
  color: rgb(46, 29, 29);
  top: 10px;
  width: 160px;
  text-align: center;
  margin-right: 0.5rem;
  border-radius: 8px;
}
.ribbon2 {
  position: fixed;
  margin: 0px 0px 0px 700px;
  background-color: rgb(37, 88, 84);
  color: rgb(51, 30, 30);
  top: 10px;
  width: 160px;
  text-align: center;
  margin-right: 0.5rem;
  border-radius: 8px;
}
.ribbon:hover {
  position: fixed;
  margin: 0px 0px 0px 430px;
  background-color: rgb(67, 68, 63);
  color: rgb(150, 144, 144);
  top: 10px;
  width: 160px;
  text-align: center;
}
.ribbon2:hover {
  position: fixed;
  margin: 0px 0px 0px 700px;
  background-color: rgb(67, 68, 63);
  color: rgb(150, 144, 144);
  top: 10px;
  width: 160px;
  text-align: center;
}
.logout {
  position: fixed;
  margin: 10px 0px 0px 1300px;
  background-color: #dd2e2e;
  color: rgb(253, 252, 252);
  top: 10px;
  /* height: 35px; */
  width: 150px;
  text-align: center;
  margin-right: 0.5rem;
  border-radius: 8px;
}
.logout:hover {
  position: fixed;
  margin: 10px 0px 0px 1300px;
  background-color: rgb(255, 255, 255);
  color: rgb(2, 0, 0);
  top: 10px;
  /* height: 35px; */
  width: 150px;
  text-align: center;
  margin-right: 0.5rem;
  border-radius: 8px;
}
.logout2 {
  position: fixed;
  margin: 10px 0px 0px 1300px;
  background-color: #ff0000;
  color: white;
  top: 10px;
  /* height: 35px; */
  width: 150px;
  text-align: center;
  margin-right: 0.5rem;
  border-radius: 8px;
}
.logout2:hover {
  position: fixed;
  margin: 10px 0px 0px 1300px;
  background-color: rgb(195, 255, 0);
  color: rgb(255, 0, 0);
  top: 10px;
  /* height: 35px; */
  width: 150px;
  text-align: center;
  margin-right: 0.5rem;
  border-radius: 8px;
}
.search {
  position: fixed;
  margin: 15px 0px 0px 250px;
  top: 9px;
  width: 100px;
  text-align: center;
}
.search:hover {
  position: fixed;
  background-color: rgb(75, 177, 177);
  margin: 15px 0px 0px 250px;
  top: 9px;
  width: 100px;
  text-align: center;
}
.searchbar {
  position: fixed;
  margin: 15px 0px 0px 100px;
  top: 9px;
  width: 150px;
  text-align: center;
}
.jj {
  position: fixed;
  margin: 0px 0px 0px -250px;
  top: 40px;
}
#container {
  position: relative;
  width: 80%;
  margin: 5% auto;
  background-color: black;
  box-shadow: -2px -2px 5px white, 2px -2px 5px white;
}
#container > nav {
  background-color: black;
  width: 100%;
  display: flex;
  max-height: 60px;
}
/* .logo {
  position: fixed;
  margin: -10px 0px 0px -730px;
  top: 10px;
  height: 60px;
  padding: 0 0px;
  background-color: white;
  width: 70px;
} */
#container > nav > ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
  display: flex;
  position: absolute;
  right: 50px;
  /*   min-width:60%; */
}
#container > nav > ul > li {
  background-color: black;
  line-height: 60px;
  margin: 0 0px;
  padding: 0;
  text-align: center;
  display: inline-block;

  /*   background-color:green; */
  min-width: 120px;
}
#container > nav > ul > li > a {
  position: relative;
  background-color: red;
  margin: 0 20px;
  color: white;
}
#container > nav > ul > li:hover {
  border-bottom: 2px solid white;
  background-color: #0088ff;
}
#container > nav > ul > .dropdown:hover {
  border-bottom: none;
}
#container > nav > ul > .dropdown:hover > .dd {
  display: block;
}
.dropdown:hover > a .fa-caret-down {
  display: none;
}
a {
  text-decoration: none;
}

#container > nav > ul > li > div {
  position: absolute;
  padding: 0 10px;

  background-color: black;
  display: none;
  background-color: aliceblue;
  min-width: 100px;
}

#container > nav > ul > li > div > ul {
  margin: 0px 0 10px 0;
  padding: 0;
  list-style: none;
}
#u_a_c {
  position: relative;
  width: 100%;
  /*   background-color:red; */
}
#up_arrow {
  position: relative;
  width: 20px;
  height: 20px;
  left: 42%;
  top: -10px;
  background-color: aliceblue;
  transform: rotate(45deg);
}
#container > nav > ul > li > div > ul > li:hover {
  background-color: rgba(243, 182, 182, 0.2);
}
#container > nav > ul > li > div > ul > li > a {
  padding: 5px;
  color: black;
}
</style>
