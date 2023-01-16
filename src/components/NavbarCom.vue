<template>
  <!-- component -->
  <nav class="body" id="container">
    <div class="">
      <a href="/"><img id="logo" src="@/assets/logo2.png" alt="a" /></a>
      <div class="">
        <!-- <span class="font-semibold text-xl tracking-tight">ANIME-W</span> -->
        <!-- <img class="h-20 w-50" src="../assets/ANIME-W.png" alt="" /> -->
      </div>
      <div class="">
        <button id="" class="">
          <svg
            class="fill-current h-3 w-3"
            viewBox="0 0 20 20"
            xmlns="http://www.w3.org/2000/svg"
          >
            <title>Menu</title>
            <path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z" />
          </svg>
        </button>
      </div>
    </div>

    <div class="">
      <div class="">
        <button @click="$router.push({ path: '/' })" class="ribbon2">
          Anime
        </button>

        <button @click="$router.push({ path: '/about' })" class="ribbon">
          Bookmark
        </button>
      </div>
      <dropdown
        v-model="select_search"
        :options="choice"
        :selected="choose"
        v-on:updateOption="methodToRunOnSelect"
      ></dropdown>
      <!-- This is an example component -->
      <div class="">
        <Form @submit="check_search" :validation-schema="schema">
          <Field
            class="search"
            type="input"
            name="input"
            placeholder="Search"
          />
          <button type="submit" class="jj">
            <svg
              class="text-gray-600 h-4 w-4 fill-current"
              xmlns="http://www.w3.org/2000/svg"
              version="1.1"
              id="Capa_1"
              x="0px"
              y="0px"
              viewBox="0 0 56.966 56.966"
              style="enable-background: new 0 0 56.966 56.966"
              xml:space="preserve"
              width="12px"
              height="12px"
            >
              <path
                d="M55.146,51.887L41.588,37.786c3.486-4.144,5.396-9.358,5.396-14.786c0-12.682-10.318-23-23-23s-23,10.318-23,23  s10.318,23,23,23c4.761,0,9.298-1.436,13.177-4.162l13.661,14.208c0.571,0.593,1.339,0.92,2.162,0.92  c0.779,0,1.518-0.297,2.079-0.837C56.255,54.982,56.293,53.08,55.146,51.887z M23.984,6c9.374,0,17,7.626,17,17s-7.626,17-17,17  s-17-7.626-17-17S14.61,6,23.984,6z"
              />
            </svg>
          </button>
        </Form>
      </div>
      <div class="">
        <p class="user">
          {{ GStore.currentUser.username }}
        </p>
        <button
          v-if="!GStore.currentUser"
          @click="$router.push('login')"
          class="r"
        >
          Login
        </button>

        <button v-if="GStore.currentUser" @click="logout" class="logout">
          Logout
        </button>
      </div>
    </div>
  </nav>
</template>
<script>
import AuthService from '@/service/AuthService.js'
import AnimeService from '@/service/AnimeService.js'
import { Form, Field } from 'vee-validate'
import * as yup from 'yup'
import dropdown from 'vue-dropdowns'
export default {
  inject: ['GStore'],
  name: 'NavBar',
  components: {
    Form,
    Field,
    dropdown
  },
  data() {
    const schema = yup.object().shape({
      input: yup.string()
    })
    return {
      schema,
      select_search: null,
      choice: [{ name: 'Title' }, { name: 'Description' }],
      choose: {
        name: 'Selected search'
      }
    }
  },
  methods: {
    logout() {
      AuthService.logout()
      this.$router.go()
    },
    methodToRunOnSelect(payload) {
      this.choose = payload
    },
    check_search(input) {
      if (
        this.choose.name == 'Selected search' ||
        this.choose.name == 'Title'
      ) {
        AnimeService.getAnimeList(input)
        setTimeout(() => this.$router.push('animeList'), 200)
      } else {
        AnimeService.getAnimeList_description(input)
        setTimeout(() => this.$router.push('animeList'), 200)
      }
    }
  }
}
</script>
<style scoped>
/* .r {
  top: 20%;
  left: 40%;
  margin-left: -250px;
} */
* {
  margin: 0;
  padding: 0;
}
.body {
  background-color: #0088ff;
  font-family: 'Raleway', sans-serif;
}
.ribbon {
  position: absolute;
  background-color: red;
  color: white;
  top: 40px;
  width: 160px;
  text-align: center;
  margin-right: 0.5rem;
  border-radius: 8px;
}
.ribbon2 {
  position: absolute;
  margin: 0px 0px 0px -170px;
  background-color: red;
  color: white;
  top: 40px;
  width: 160px;
  text-align: center;
  margin-right: 0.5rem;
  border-radius: 8px;
}
.ribbon:hover {
  position: absolute;
  background-color: rgb(195, 255, 0);
  color: rgb(255, 0, 0);
  top: 40px;
  width: 160px;
  text-align: center;
}
.ribbon2:hover {
  position: absolute;
  margin: 0px 0px 0px -170px;
  background-color: rgb(195, 255, 0);
  color: rgb(255, 0, 0);
  top: 40px;
  width: 160px;
  text-align: center;
}
.user {
  position: absolute;
  margin: 0px 0px 0px 950px;
  background-color: #0088ff;
  color: white;
  top: 40px;
  width: 160px;
  text-align: center;
  margin-right: 0.5rem;
  border-radius: 8px;
}
.logout {
  position: absolute;
  margin: 0px 0px 0px 250px;
  background-color: #ff0000;
  color: white;
  top: 40px;
  width: 95px;
  text-align: center;
  margin-right: 0.5rem;
  border-radius: 8px;
}
.logout:hover {
  position: absolute;
  margin: 0px 0px 0px 250px;
  background-color: rgb(195, 255, 0);
  color: rgb(255, 0, 0);
  top: 40px;
  width: 95px;
  text-align: center;
  margin-right: 0.5rem;
  border-radius: 8px;
}
.search {
  position: absolute;
  margin: 0px 0px 0px -450px;
  background-color: rgb(195, 255, 0);
  color: rgb(255, 0, 0);
  top: 40px;
  width: 200px;
  text-align: center;
  margin-right: 0.5rem;
  border-radius: 8px;
}
.jj {
  position: absolute;
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
  width: 100%;
  display: flex;
  max-height: 60px;
}
#logo {
  margin: 0px 1500px 0px 0px;
  line-height: 20px;
  padding: 0 0px;
  background-color: white;
  width: 100px;
}
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
  /*   background-color:red; */
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
  background-color: rgba(0, 0, 0, 0.2);
}
#container > nav > ul > li > div > ul > li > a {
  padding: 5px;
  color: black;
}
</style>
