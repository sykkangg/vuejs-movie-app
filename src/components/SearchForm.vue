<template>
  <div class="">
    <input placeholder="영화명을 입력하세요" type="text" v-model="searchKeyword" />
    <p>검색 결과: "{{ searchKeyword }}"</p>
    <button @click="handleSearch">검색</button>
    <button v-if="searchKeyword.length > 0">초기화</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const searchKeyword = ref('')

const emit = defineEmits(['search', 'clear'])

const handleSearch = () => {
  if (searchKeyword.value.trim()) {
    console.log('키워드 emit')
    emit('search', searchKeyword.value)
  }
}
</script>
