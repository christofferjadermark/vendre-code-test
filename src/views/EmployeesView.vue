<script setup>
import { ref, onMounted } from 'vue'
import '../assets/main.css'

const employees = ref([])
const currentPage = ref(1)
const totalPages = ref(2)
onMounted(() => {
  fetchData()
})

function fetchData() {
  fetch(`https://reqres.in/api/users?page=${currentPage.value}`, {
    method: 'GET',
    headers: {
      'Content-Type': 'application/json'
    }
  })
    .then((response) => response.json())
    .then((result) => {
      employees.value = result.data
      console.log(employees.value)
    })
}

function previousPage() {
  if (currentPage.value > 1) {
    currentPage.value--
    fetchData()
  }
}

function nextPage() {
  currentPage.value++
  fetchData()
}
</script>

<style scoped>
.employees {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  height: 200px;
  background-color: #925d6e;
  color: white;
  border-radius: 20px;
  font-family: 'basic-sans', sans-serif;
  transition: all 0.3s ease-in-out;
  width: 200px;
}

.employees:hover {
  transform: scale(1.1);
}

.user-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 20px;
}

.name {
  margin: 0;
}

.profile-img {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  margin-top: 10px;
}

.pagination {
  display: flex;
  justify-content: center;
  gap: 30px;
  align-items: center;
  margin-top: 40px;
}

.emailus-text {
  text-align: center;
  font-family: 'basic-sans', sans-serif;
  font-weight: 700;
  font-size: 24px;
  line-height: 36px;
  letter-spacing: 0.1rem;
  margin-top: 40px;
}
.button-container {
  margin: 0 5px;
  padding: 5px 10px;
  border: 1px solid #925d6e;
  border-radius: 5px;
  background-color: #925d6e;
  color: white;
  font-family: 'basic-sans', sans-serif;
  cursor: pointer;
}

a {
  text-decoration: none;
  color: white;
  cursor: pointer;
}
</style>

<template>
  <h1 class="emailus-text">You're welcome to email us if you have any questions!</h1>
  <div class="user-container">
    <div v-for="employee in employees" v-bind:key="employee" class="employees">
      <img class="profile-img" :src="employee.avatar" alt="" />
      <div>
        <h3 class="name">{{ employee.first_name }} {{ employee.last_name }}</h3>
        <a :href="`mailto:${employee.email}`">{{ employee.email }}</a>
      </div>
    </div>
  </div>
  <div class="pagination">
    <button class="button-container" :disabled="currentPage === 1" @click="previousPage">
      Previous
    </button>
    <span>{{ currentPage }}</span>
    <button class="button-container" :disabled="currentPage === totalPages" @click="nextPage">
      Next
    </button>
  </div>
</template>
