<script setup>
import { ref } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import MovieCard from './components/MovieCard.vue'

const handleMovieClick = (movieData) => {
  console.log('부모가 받은 데이터', movieData)
  alert(`${movieData.title}을(를) 클릭하셨습니다! \n 평점: ${movieData.rate} ⭐`)
}

const movies = ref([
  {
    id: 1,
    title: '쿵푸팬더 4',
    rate: '8.5',
    year: '2024',
    overview: '평화의 계곡을 지키던 용의 전사 포가 새로운 모험을 떠납니다.',
    poster: 'https://image.tmdb.org/t/p/w500/kDp1vUBnMpe8ak4rjgl3cLELqjU.jpg',
  },
  {
    id: 2,
    title: '베놈: 라스트 댄스',
    rate: '7.2',
    year: '2024',
    overview: '에디와 베놈의 마지막 이야기가 펼쳐집니다.',
    poster: 'https://image.tmdb.org/t/p/w500/aosm8NMQ3UyoBVpSxyimorCQykC.jpg',
  },
  {
    id: 3,
    title: '겨울왕국',
    rate: '7.4',
    year: '2013',
    overview: '자매의 사랑과 마법이 펼쳐지는 디즈니 애니메이션.',
    poster: 'https://image.tmdb.org/t/p/w500/kgwjIb0CuS4ZzNRhlTu7LqKhGP3.jpg',
  },
  {
    id: 4,
    title: '인사이드 아웃 2',
    rate: '7.8',
    year: '2024',
    overview: '라일리의 새로운 감정들이 등장합니다.',
    poster: 'https://image.tmdb.org/t/p/w500/vpnVM9B6NMmQpWeZvzLvDESb2QY.jpg',
  },
  {
    id: 5,
    title: '듄: 파트 2',
    rate: '8.3',
    year: '2024',
    overview: '폴 아트레이드의 대서사시가 계속됩니다.',
    poster: 'https://image.tmdb.org/t/p/w500/1pdfLvkbY9ohJlCjQH2CZjjYVvJ.jpg',
  },
  {
    id: 6,
    title: '위키드',
    rate: '7.9',
    year: '2024',
    overview: '오즈의 마법사 이전의 이야기를 담은 뮤지컬 판타지.',
    poster: 'https://image.tmdb.org/t/p/w500/c5Tqxeo1UpBvnAc3csUm7j3hlQl.jpg',
  },
])
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
        v-for="movie in movies"
        :key="movie.id"
        :title="movie.title"
        :rate="movie.rate"
        :year="movie.year"
        :overview="movie.overview"
        :poster="movie.poster"
        @movie-click="handleMovieClick"
      />
    </div>

    <div class="emty" v-if="movies.length === 0">
      <p>😢 영화가 없습니다.</p>
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
