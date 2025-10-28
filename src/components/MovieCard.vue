<template>
  <div class="movie-card" @click="handleClick">
    <!-- 영화 포스터 -->
    <div class="poster">
      <img
        src="https://image.tmdb.org/t/p/w500/kDp1vUBnMpe8ak4rjgl3cLELqjU.jpg"
        alt="영화 포스터"
      />
    </div>

    <!-- 영화 정보 -->
    <div class="info">
      <h3 class="title">{{ title }}</h3>
      <div class="details">
        <span class="rating">⭐ {{ rate }}</span>
        <span class="year">{{ year }}</span>
      </div>
      <p class="overview">{{ overview }}</p>
    </div>
  </div>
</template>

<script setup>
console.log('Movie Card 컴포넌트 로드 완료')

const props = defineProps({
  title: {
    type: String,
    required: true,
  },
  rate: {
    type: String,
    required: true,
  },
  year: {
    type: String,
    required: true,
  },
  overview: {
    type: String,
    required: true,
  },
})

const emit = defineEmits(['movie-click'])

const handleClick = () => {
  console.log(`${props.title} 카드가 클릭됨!`)

  emit('movie-click', {
    title: props.title,
    rate: props.rate,
    year: props.year,
    overview: props.overview,
  })
}
</script>

<style scoped>
.movie-card {
  background: white;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
  cursor: pointer;
}

.movie-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.2);
}

.poster {
  width: 100%;
  height: 300px;
  overflow: hidden;
}

.poster img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.info {
  padding: 15px;
}

.title {
  margin: 0 0 10px 0;
  font-size: 18px;
  font-weight: bold;
  color: #333;
}

.details {
  display: flex;
  gap: 15px;
  margin-bottom: 10px;
  font-size: 14px;
}

.rating {
  color: #f59e0b;
  font-weight: 600;
}

.year {
  color: #6b7280;
}

.overview {
  font-size: 14px;
  color: #6b7280;
  line-height: 1.5;
  margin: 0;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>
