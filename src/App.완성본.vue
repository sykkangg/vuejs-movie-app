<script setup>
import { ref, computed } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import MovieCard from './components/MovieCard.vue'
import SearchForm from './components/SearchForm.vue'

const handleMovieClick = (movieData) => {
  console.log('부모가 받은 데이터', movieData)
  alert(`${movieData.title}을(를) 클릭하셨습니다! \n 평점: ${movieData.rate} ⭐`)
}

// 검색어 상태
const searchQuery = ref('')

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

// computed로 검색 필터링
const filteredMovies = computed(() => {
  if (!searchQuery.value) {
    return movies.value
  }
  return movies.value.filter((movie) =>
    movie.title.toLowerCase().includes(searchQuery.value.toLowerCase()),
  )
})

// 검색 핸들러
const handleSearch = (query) => {
  searchQuery.value = query
  console.log('검색어:', query)
}

// 검색 초기화
const handleClear = () => {
  searchQuery.value = ''
  console.log('검색 초기화')
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
    <!-- 검색 폼 컴포넌트 -->
    <SearchForm @search="handleSearch" @clear="handleClear" />

    <!-- 검색 결과 개수 표시 -->
    <div class="result-info">
      <p v-if="searchQuery">"{{ searchQuery }}" 검색 결과: {{ filteredMovies.length }}개</p>
      <p v-else>전체 영화: {{ movies.length }}개</p>
    </div>

    <div class="movie-grid" v-if="filteredMovies.length > 0">
      <MovieCard
        v-for="movie in filteredMovies"
        :key="movie.id"
        :title="movie.title"
        :rate="movie.rate"
        :year="movie.year"
        :overview="movie.overview"
        :poster="movie.poster"
        @movie-click="handleMovieClick"
      />
    </div>

    <div v-else class="empty">
      <p>😢 "{{ searchQuery }}"에 대한 검색 결과가 없습니다.</p>
      <button @click="handleClear" class="reset-button">전체 보기</button>
    </div>
  </main>

  <RouterView />
</template>

<style scoped>
header {
  background: #1f2937;
  color: white;
  padding: 20px;
  margin-bottom: 30px;
}

header h1 {
  margin: 0 0 15px 0;
  text-align: center;
}

nav {
  display: flex;
  gap: 20px;
  justify-content: center;
}

nav a {
  color: white;
  text-decoration: none;
  padding: 8px 16px;
  border-radius: 6px;
  transition: background 0.3s;
}

nav a:hover {
  background: rgba(255, 255, 255, 0.1);
}

nav a.router-link-exact-active {
  background: #3b82f6;
}

main {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 20px;
}

.result-info {
  text-align: center;
  margin-bottom: 20px;
  font-size: 16px;
  color: #4b5563;
  font-weight: 500;
}

.movie-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 30px;
}

.empty {
  text-align: center;
  padding: 80px 20px;
}

.empty p {
  font-size: 20px;
  color: #6b7280;
  margin-bottom: 20px;
}

.reset-button {
  padding: 12px 24px;
  background: #3b82f6;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  cursor: pointer;
  transition: all 0.3s;
}

.reset-button:hover {
  background: #2563eb;
  transform: translateY(-2px);
}
</style>
