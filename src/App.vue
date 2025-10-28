<script setup>
import { RouterLink, RouterView } from 'vue-router'
import MovieCard from './components/MovieCard.vue'

const handleMovieClick = (movieData) => {
  console.log('부모가 받은 데이터', movieData)
  alert(`${movieData.title}을(를) 클릭하셨습니다! \n 평점: ${movieData.rate} ⭐`)
}
</script>

<template>
  <header>
    <div class="wrapper">
      <h1>🎬 영화 검색 앱</h1>
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <main>
    <div class="movie-grid">
      <MovieCard
        title="쿵푸팬더"
        rate="3"
        year="2024"
        overview="영화 설명입니다."
        @movie-click="handleMovieClick"
      />
      <MovieCard
        title="베놈"
        rate="3"
        year="2024"
        overview="영화 설명입니다."
        @movie-click="handleMovieClick"
      />
      <MovieCard
        title="겨울왕국"
        rate="4"
        year="2024"
        overview="영화 설명입니다."
        @movie-click="handleMovieClick"
      />
    </div>
  </main>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
