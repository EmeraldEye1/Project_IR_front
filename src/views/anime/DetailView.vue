<template>
  <div v-for="anime in GStore.details" :key="anime.mal_id">
    <div class="dark:bg-gray-800 dark:text-gray-50">
      <div id="detail">
        <img class="img" :src="anime.images" alt="anime_image" />
        <h2>{{ anime.title }}</h2>
        <p><span>Synopsis</span><br /></p>

        <p class="text">{{ anime.synopsis }}</p>
        <p></p>
        <p><span>Genres</span><br /></p>

        <p class="text">{{ anime.genres }}</p>
        <p></p>
      </div>
    </div>
  </div>
  <dropdown
    v-model="select"
    :options="choice"
    :selected="choose"
    v-on:updateOption="methodToRunOnSelect"
  ></dropdown>
  <button @click="addBookmark()">Add to favorite</button>
</template>
<script>
import AnimeService from '../../service/anime/AnimeService.js';
import dropdown from 'vue-dropdowns';
export default {
  inject: ['GStore'],
  name: 'DetailView',
  components: {
    dropdown
  },
  data() {
    return {
      select: null,
      choice: [
        { name: '1' },
        { name: '2' },
        { name: '3' },
        { name: '4' },
        { name: '5' }
      ],
      choose: {
        name: '1'
      }
    };
  },
  methods: {
    addBookmark() {
      AnimeService.addBookmark(
        this.GStore.currentUser.id,
        this.GStore.details.malid,
        this.choose.name
      ).then(() => {
        alert('Success add favorite');
      });
    },
    methodToRunOnSelect(payload) {
      this.choose = payload;
    }
  }
};
</script>
<style scoped>
span,
h2 {
  font-weight: bold;
  color: rgb(254, 254, 254);
}
.text {
  color: rgb(8, 6, 6);
}
img {
  margin: 100px 0 0 0;
}
</style>
