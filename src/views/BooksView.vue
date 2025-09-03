<template>
  <div class="container">
    <h1 class="title">CRUD de Libros</h1>

    <!-- Formulario -->
    <form @submit.prevent="saveBook" class="form-container">
      <input v-model="bookForm.id" type="number" placeholder="ID" :disabled="editing" />
      <input v-model="bookForm.title" placeholder="Título" />
      <input v-model="bookForm.author" placeholder="Autor" />
      <input v-model="bookForm.year" type="number" placeholder="Año" />
      <input v-model="bookForm.price" type="number" step="0.01" placeholder="Precio" />
      <input v-model="bookForm.stock" type="number" placeholder="Stock" />
      <textarea v-model="bookForm.description" placeholder="Descripción"></textarea>
      <button type="submit" class="btn-submit">
        {{ editing ? 'Actualizar' : 'Crear' }}
      </button>
    </form>

    <!-- Lista de libros -->
    <div class="table-wrapper">
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Título</th>
            <th>Autor</th>
            <th>Año</th>
            <th>Precio</th>
            <th>Stock</th>
            <th>Acciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="book in books" :key="book.id">
            <td style="color: black;">{{ book.id }}</td>
            <td style="color: black;">{{ book.title }}</td>
            <td style="color: black;">{{ book.author }}</td>
            <td style="color: black;">{{ book.year }}</td>
            <td style="color: black;">{{ book.price }}</td>
            <td style="color: black;">{{ book.stock }}</td>
            <td style="color: black;" class="actions">
              <button @click="editBook(book)" class="btn-edit">Editar</button>
              <button @click="deleteBook(book.id)" class="btn-delete">Eliminar</button>
            </td>
          </tr>
          <tr v-if="books.length === 0">
            <td colspan="7" class="empty-msg">No hay libros registrados</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const books = ref([])
const bookForm = ref({ id: '', title: '', author: '', year: '', price: '', stock: '', description: '' })
const editing = ref(false)
const API_URL = 'http://127.0.0.1:8000/books'

async function fetchBooks() {
  const res = await axios.get(API_URL)
  books.value = res.data
}

async function saveBook() {
  if (editing.value) {
    await axios.put(`${API_URL}/${bookForm.value.id}`, bookForm.value)
    editing.value = false
  } else {
    await axios.post(API_URL, bookForm.value)
  }
  resetForm()
  fetchBooks()
}

function editBook(book) {
  bookForm.value = { ...book }
  editing.value = true
}

async function deleteBook(id) {
  await axios.delete(`${API_URL}/${id}`)
  fetchBooks()
}

function resetForm() {
  bookForm.value = { id: '', title: '', author: '', year: '', price: '', stock: '', description: '' }
}

onMounted(fetchBooks)
</script>

<style scoped>
/* Estilos base (pantallas grandes por defecto) */
.container {
  max-width: 900px;
  margin: 20px auto;
  padding: 20px;
  font-family: Arial, sans-serif;
  background: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.title {
  text-align: center;
  margin-bottom: 20px;
  font-size: 26px;
  color: #333;
}

.form-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
  margin-bottom: 20px;
}

.form-container input,
.form-container textarea {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 100%;
}

.form-container textarea {
  grid-column: span 2;
  resize: none;
  min-height: 80px;
}

.btn-submit {
  grid-column: span 2;
  padding: 10px;
  background: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.btn-submit:hover {
  background: #0056b3;
}

.table-wrapper {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  padding: 10px;
  border: 1px solid #ddd;
  text-align: center;
}

thead {
  background: #007bff;
  color: white;
}

tbody tr:hover {
  background: #f2f2f2;
}

.empty-msg {
  text-align: center;
  color: #777;
}

.actions {
  display: flex;
  gap: 8px;
  justify-content: center;
}

.btn-edit {
  background: #ffc107;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
}

.btn-edit:hover {
  background: #e0a800;
}

.btn-delete {
  background: #dc3545;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  color: white;
  cursor: pointer;
}

.btn-delete:hover {
  background: #c82333;
}

/* Media Queries */

/* Pantallas pequeñas (móviles) */
@media (max-width: 600px) {
  .form-container {
    grid-template-columns: 1fr;
  }

  .btn-submit {
    grid-column: span 1;
  }

  table {
    font-size: 14px;
  }

  th, td {
    padding: 6px;
  }

  .title {
    font-size: 22px;
  }
}

/* Pantallas medianas (tabletas) */
@media (min-width: 601px) and (max-width: 900px) {
  .form-container {
    grid-template-columns: 1fr 1fr;
  }

  .title {
    font-size: 24px;
  }
}


</style>


