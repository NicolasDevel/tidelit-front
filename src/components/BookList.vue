<template>
  <div class="container">
    <header class="header">
      <h1>TideLit — Books</h1>
      <button @click="loadBooks" :disabled="loading">
        {{ loading ? 'Refreshing...' : 'Refresh' }}
      </button>
    </header>

    <main>
      <p v-if="error" class="error">{{ error }}</p>

      <ul v-if="books.length" class="book-list">
        <li v-for="book in books" :key="book.title" class="book-item">
          <div>
            <div class="title">{{ book.title }}</div>
            <div class="meta">{{ book.author }} — {{ book.published_year }}</div>
          </div>
          <div class="rating">
            <strong v-if="book.average_rating !== null">{{ book.average_rating }}</strong>
            <em v-else>null</em>
          </div>
        </li>
      </ul>

      <p v-else-if="!loading">No books found.</p>
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import api from './axios/client'

const books = ref([])
const loading = ref(false)
const error = ref(null)

async function loadBooks() {
  loading.value = true
  error.value = null
  try {
    const res = await api.get('/books')
    books.value = res.data.data.map(b => ({
      title: b.title,
      author: b.author,
      published_year: b.published_year,
      average_rating: b.average_rating !== null ? Number(b.average_rating) : null
    }))
  } catch (err) {
    console.error(err)
    if (err.response && err.response.data && err.response.data.message) {
      error.value = `API: ${err.response.data.message}`
    } else {
      error.value = 'Could not load books. Check backend and CORS.'
    }
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  loadBooks()
})
</script>

<style>
.container {
  max-width: 800px;
  margin: 2rem auto;
  padding: 0 1rem;
  font-family: system-ui, sans-serif;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}

button {
  padding: .5rem .75rem;
  border-radius: 6px;
  border: 1px solid #ccc;
  background: #fafafa;
  cursor: pointer;
}

.book-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.book-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  padding: .75rem;
  border: 1px solid #eee;
  border-radius: 6px;
  margin-bottom: .5rem;
}

.title {
  font-weight: 600
}

.meta {
  color: #666;
  font-size: .9rem
}

.rating {
  min-width: 80px;
  text-align: right
}

.error {
  color: #c00;
  margin-bottom: 1rem
}
</style>
