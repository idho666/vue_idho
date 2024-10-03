<script setup>
import { ref } from "vue";
import axios from "axios";

const baseUrl = import.meta.env.VITE_RESTAURANT_BASE_URL;

const restaurantList = ref([]);

// Fetch data from API
const fetchData = async () => {
  try {
    const { data } = await axios.get(`${baseUrl}/list`);

    restaurantList.value = data.restaurants; // Store the data in the reactive variable
  } catch (error) {
    console.error("Error fetching data:", error);
  }
};

fetchData();
</script>

<template>
  <table>
    <thead>
      <tr>
        <th>Nama</th>
        <th>Description</th>
        <th>Picture ID</th>
        <th>City</th>
        <th>Rating</th>
      </tr>
    </thead>
    <tbody>
      <!-- Loop through the restaurant list and display the data -->
      <tr v-for="restaurant in restaurantList" :key="restaurant.id">
        <td>{{ restaurant.name }}</td>
        <td>{{ restaurant.description }}</td>
        <td>{{ restaurant.pictureId }}</td>
        <td>{{ restaurant.city }}</td>
        <td>{{ restaurant.rating }}</td>
      </tr>
    </tbody>
  </table>
</template>

<style scoped>
table {
  width: 600px;
  border-collapse: collapse;
  margin-top: 20px;
}

th,
td {
  padding: 12px;
  text-align: left;
  border: 1px solid #ddd;
}

th {
  background-color: #4caf50;
  color: white;
  font-weight: bold;
}

tr:nth-child(even) {
  background-color: #f2f2f2;
}

tr:hover {
  background-color: #ddd;
}

.error {
  color: red;
}
</style>
