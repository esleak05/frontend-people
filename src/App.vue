<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'

const peoples = ref([])

const fetchPeoples = async () => {
  try {
    const response = await axios.get('https://backend-crore.34.144.234.247.nip.io/people')

    peoples.value = response.data
    console.log(peoples.value)
  } catch (error) {
    console.error('Error al obtener los datos', error)
  }
}

onMounted(() => {
  fetchPeoples()
})
</script>

<template>
  <div class="container">
    <v-toolbar title="People app"></v-toolbar>
    <v-table>
      <thead>
        <tr>
          <th class="text-left">Name</th>
          <th class="text-left">Age</th>
          <th class="text-center">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="people in peoples" :key="people.name">
          <td>{{ people.name }}</td>
          <td>{{ people.age }}</td>
          <td>
            <v-container>
              <v-row align="center" justify="center">
                <v-col cols="auto">
                  <v-btn class="ma-2" color="primary">
                    view
                    <v-icon icon="mdi-checkbox-marked-circle" end></v-icon>
                  </v-btn>
                </v-col>

                <v-col cols="auto">
                  <v-btn density="compact">update</v-btn>
                </v-col>

                <v-col cols="auto">
                  <v-btn density="compact">delete</v-btn>
                </v-col>
              </v-row>
            </v-container>
          </td>
        </tr>
      </tbody>
    </v-table>
  </div>
</template>

<style>
.container {
  padding: 50px;
}
</style>
