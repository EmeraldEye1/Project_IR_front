<template>
  <router-link
    class="anime-link"
    :to="{ name: 'DetailView', params: { id: anime.mal_id } }"
  >
    <div class="anime-card flex items-center justify-center">
      <img
        :src="anime.images"
        class="rounded shadow h-90 w-80"
        alt="anime_image"
      />
      <h4>{{ anime.title }}</h4>
    </div>
  </router-link>
</template>
<script>
export default {
  name: 'AnimeCard',
  props: {
    anime: {
      type: Object,
      required: true
    }
  }
};
</script>
<style scoped>
.anime-card {
  position: cover;
  margin: 0px 0 0 100px;
  /* padding: 50px; */
  width: 250px;
  cursor: pointer;
  border: 5px solid #fad61f;
  margin-bottom: 18px;
}
.anime-card:hover {
  transform: scale(1.01);
  box-shadow: 0 3px 12px 0 rgba(252, 0, 0, 0.459);
}
.anime-link {
  color: #000000;
  text-decoration: none;
}
</style>
