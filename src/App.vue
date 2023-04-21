<template>
  <div class="todo-list">
    <h1>Aplikasi Booking Tiket Pesawat</h1>
    <form @submit.prevent="addTodo">
      <div class="form-group">
        <label for="nik">NIK Pemesan:</label>
        <input type="text" id="nik" v-model="newTodo" placeholder="Masukkan NIK Pemesan" required />
      </div>
      <div class="form-group">
        <label for="nama">Nama Pemesan:</label>
        <input type="text" id="nama" v-model="newPeminjam" placeholder="Masukkan nama pemesan" required />
      </div>
      <div class="form-group">
        <label for="tanggal">Tanggal dan Waktu:</label>
        <input type="datetime-local" id="tanggal" v-model="newDate" required />
      </div>
      <div class="form-group">
        <label for="asal">Asal:</label>
        <input type="text" id="asal" v-model="newAsal" placeholder="Asal" required />
      </div>
      <div class="form-group">
        <label for="tujuan">Tujuan:</label>
        <input type="text" id="tujuan" v-model="newTujuan" placeholder="Tujuan" required />
      </div>
      <button type="submit" class="tambahkan">Tambahkan</button>
    </form>
    <h2>List Item</h2>
    <div class="tengah">
      <ul>
        <li v-for="(todo, index) in todos" :key="todo.id" :class="{ 'done': todo.done }">
          <input type="checkbox" v-model="todo.done" />
          <div class="todo-item">
            <span>{{ todo.text }}</span>
            <span>{{ todo.date }}</span>
            <span>{{ todo.asal }}</span>
            <span>{{ todo.tujuan }}</span>
            <span>({{ todo.peminjam }})</span>
          </div>
          <button @click="removeTodo(index)">Remove</button>
        </li>
      </ul>
      <div v-if="todos.length > 0">
        <button @click="removeAllTodos" class="remove-all">Remove All</button>
      </div>
      <div v-else>
        <p>Tidak ada item yang ditambahkan.</p>
      </div>
    </div>
    <footer>
      <p>&copy; Slamet Kurniawan 2023</p>
    </footer>
  </div>
</template>

<script>export default {
  data() {
    return {
      newTodo: '',
      newPeminjam: '',
      newDate: '',
      newAsal: '',
      newTujuan: '',
      todos: [],
    };
  },
  methods: {
    addTodo() {
      if (
        this.newTodo.trim().length === 0 ||
        this.newPeminjam.trim().length === 0 ||
        !this.newDate ||
        this.newAsal.trim().length === 0 ||
        this.newTujuan.trim().length === 0
      ) {
        return;
      }
      this.todos.push({
        text: this.newTodo,
        peminjam: this.newPeminjam,
        done: false,
        date: new Date(this.newDate).toLocaleString('id-ID', {
          weekday: 'long',
          day: 'numeric',
          month: 'long'
        }),
        asal: this.newAsal,
        tujuan: this.newTujuan,
      });
      this.newTodo = '';
      this.newPeminjam = '';
      this.newDate = '';
      this.newAsal = '';
      this.newTujuan = '';
    },
    removeTodo: function(index) {
      this.todos.splice(index, 1);
    },
    removeAllTodos: function() {
      this.todos = [];
    },
  },
};
</script>


<style>
h1{
  color: #000000;
}

h2{
  color: #000000;
}
  .todo-list {
    font-family: sans-serif;
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
  }
  body {
    background-image: url(https://cdn-2.tstatic.net/batam/foto/bank/images/citilink.jpg);
    background-size: cover;
  }
  .todo-list h1 {
text-align: center;
margin-bottom: 30px;
}

form {
display: flex;
flex-direction: column;
margin-bottom: 20px;
}

input[type='text'],
select,
input[type='datetime-local'] {
margin-bottom: 10px;
padding: 10px;
border-radius: 5px;
border: none;
font-size: 16px;
}

input[type='text']:focus,
select:focus,
input[type='datetime-local']:focus {
outline: none;
box-shadow: 0 0 5px 2px #5bc0de;
}

button[type='submit'] {
background-color: #5bc0de;
color: #fff;
border: none;
border-radius: 5px;
padding: 10px;
font-size: 16px;
cursor: pointer;
}

button[type='submit']:hover {
background-color: #31d570;
}

.tambahkan {
margin-top: 10px;
align-self: flex-end;
}

h2 {
margin-bottom: 10px;
}

ul {
list-style-type: none;
margin: 0;
padding: 0;
}

li {
display: flex;
align-items: center;
justify-content: space-between;
margin-bottom: 10px;
padding: 10px;
border-radius: 5px;
background-color: #fff;
box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
}

li.done {
background-color: #e6e6e6;
text-decoration: line-through;
}

input[type='checkbox'] {
margin-right: 10px;
cursor: pointer;
}

.remove-all {
background-color: #d9534f;
color: #fff;
border: none;
border-radius: 5px;
padding: 10px;
font-size: 16px;
cursor: pointer;
}

.remove-all:hover {
background-color: #c9302c;
}

.tengah {
display: flex;
flex-direction: column;
justify-content: center;
align-items: center;
}

footer {
margin-top: 20px;
text-align: center;
font-size: 14px;
}

footer p {
margin: 0;
padding: 0;
color: #fff;
}
</style>