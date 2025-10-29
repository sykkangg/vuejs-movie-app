# 🎯 폼 입력 바인딩 연습 가이드

## 📁 파일 구성

### 백업 파일들

- `App.완성본.vue` - 검색 기능이 완성된 버전 (참고용)
- `App.Day1완료.vue` - Day 1 완료 상태 (연습 시작점)
- `App.vue` - **현재 작업 파일** (Day 1 상태로 초기화됨)

## 🎓 학습 미션

### 미션 1: SearchForm 컴포넌트 만들기

`src/components/SearchForm.vue` 파일을 만들어보세요!

**구현할 기능:**

1. ✅ `v-model`로 검색어 입력받기
2. ✅ Enter 키로 검색 실행 (`@keyup.enter`)
3. ✅ 검색 버튼 클릭으로 검색
4. ✅ 초기화 버튼 (검색어 있을 때만 표시)
5. ✅ 부모에게 `search`, `clear` 이벤트 발생

**힌트:**

```vue
<template>
  <div class="search-container">
    <input v-model.trim="searchText" @keyup.enter="handleSearch" placeholder="영화 제목 입력" />
    <button @click="handleSearch">검색</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const searchText = ref('')
const emit = defineEmits(['search'])

const handleSearch = () => {
  // TODO: emit으로 검색어 전달
}
</script>
```

---

### 미션 2: App.vue에서 검색 기능 연결

**구현할 기능:**

1. ✅ SearchForm 컴포넌트 import
2. ✅ `searchQuery` ref 만들기
3. ✅ `computed`로 `filteredMovies` 만들기
4. ✅ `handleSearch` 함수 구현
5. ✅ template에서 `filteredMovies` 사용

**힌트:**

```vue
<script setup>
import { ref, computed } from 'vue'
import SearchForm from './components/SearchForm.vue'

const searchQuery = ref('')

const filteredMovies = computed(() => {
  if (!searchQuery.value) {
    return movies.value
  }
  // TODO: filter 로직
})

const handleSearch = (query) => {
  // TODO: searchQuery 업데이트
}
</script>
```

---

### 미션 3: 검색 결과 UI 개선

1. ✅ 검색 결과 개수 표시
2. ✅ 검색 결과 없을 때 메시지
3. ✅ 초기화 버튼 추가

---

## 🆘 막힐 때

1. **콘솔 확인**: F12 눌러서 에러 메시지 보기
2. **완성본 참고**: `App.완성본.vue` 열어서 비교
3. **단계별 진행**: 한 번에 하려고 하지 말고 하나씩!

---

## ✅ 체크리스트

- [ ] SearchForm.vue 파일 생성
- [ ] v-model로 입력 받기
- [ ] emit로 부모에게 이벤트 전달
- [ ] App.vue에서 SearchForm import
- [ ] computed로 필터링 로직
- [ ] 검색 결과 표시
- [ ] 검색 결과 없을 때 처리

---

## 🎉 완료 후

완성되면 `App.완성본.vue`와 비교해보세요!
같은 기능이 작동하면 성공! 🎊

---

## 💡 핵심 개념

### v-model

```vue
<input v-model="text" />
<!-- = -->
<input :value="text" @input="text = $event.target.value" />
```

### computed

```javascript
const filtered = computed(() => {
  return data.value.filter(...)
})
```

### emit

```javascript
// 자식
const emit = defineEmits(['search'])
emit('search', value)

// 부모
<Child @search="handleSearch" />
```

연습 화이팅! 🚀
