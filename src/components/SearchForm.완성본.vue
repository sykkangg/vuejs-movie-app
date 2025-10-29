<template>
  <div class="search-container">
    <div class="search-form">
      <!-- v-model: 양방향 바인딩 -->
      <input
        v-model.trim="searchText"
        @keyup.enter="handleSearch"
        type="text"
        placeholder="영화 제목을 입력하세요... (예: 베놈)"
        class="search-input"
      />
      <button @click="handleSearch" class="search-button">🔍 검색</button>
      <button @click="clearSearch" class="clear-button" v-if="searchText">✕ 초기화</button>
    </div>

    <!-- 검색어 실시간 표시 -->
    <p v-if="searchText" class="search-info">검색 중: "{{ searchText }}"</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// v-model로 바인딩할 반응형 데이터
const searchText = ref('')

// 이벤트 정의
const emit = defineEmits(['search', 'clear'])

// 검색 실행
const handleSearch = () => {
  if (searchText.value.trim()) {
    emit('search', searchText.value)
  }
}

// 검색 초기화
const clearSearch = () => {
  searchText.value = ''
  emit('clear')
}
</script>

<style scoped>
.search-container {
  margin-bottom: 30px;
}

.search-form {
  display: flex;
  gap: 10px;
  max-width: 700px;
  margin: 0 auto;
}

.search-input {
  flex: 1;
  padding: 14px 20px;
  font-size: 16px;
  border: 2px solid #e5e7eb;
  border-radius: 10px;
  outline: none;
  transition: all 0.3s;
}

.search-input:focus {
  border-color: #3b82f6;
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

.search-button {
  padding: 14px 28px;
  background: #3b82f6;
  color: white;
  border: none;
  border-radius: 10px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s;
  white-space: nowrap;
}

.search-button:hover {
  background: #2563eb;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(59, 130, 246, 0.4);
}

.clear-button {
  padding: 14px 20px;
  background: #ef4444;
  color: white;
  border: none;
  border-radius: 10px;
  font-size: 16px;
  cursor: pointer;
  transition: all 0.3s;
}

.clear-button:hover {
  background: #dc2626;
}

.search-info {
  text-align: center;
  margin-top: 10px;
  color: #6b7280;
  font-size: 14px;
}
</style>
