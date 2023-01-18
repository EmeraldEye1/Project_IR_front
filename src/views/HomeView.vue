<template>
  <div class="home">
    <AnimeCard
      v-for="anime in GStore.anime"
      :key="anime.mal_id"
      :anime="anime"
    ></AnimeCard>
  </div>
</template>

<script>
// @ is an alias to /src
import AnimeCard from '@/components/AnimeCard.vue';

export default {
  inject: ['GStore'],
  name: 'HomeView',
  components: {
    AnimeCard
  }
};
</script>

<style scoped>
.home {
  margin: 60px -20px -100px 0;
  background-color: lightpink;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
</style>
