<template>
  <h3> {{ title }} </h3>
  <div>
    <input v-model="nachnameField" placeholder="Name" type="text">
    <input v-model="vornameField" placeholder="Vorname" type="text">
    <input v-model="studiengangField" placeholder="Studiengang" @keyup.enter="save()">
    <button type="button" @click="save()">Save</button>
  </div>
  <div>
    <table>
      <thead>
      <tr>
        <th>Name</th>
        <th>Vorname</th>
        <th>Studigang</th>
      </tr>
      </thead>
      <tbody>
      <tr v-if="items.length === 0">
        <td colspan="2">No products yet</td>
      </tr>
      <tr v-for="item in items" :key="item.id">
        <td>{{item.nachname}}</td>
        <td>{{item.vorname}}</td>
        <td>{{item.studiengang}}</td>
      </tr>
      <tr>
        <td>{{ nachnameField }}</td>
        <td>{{ vornameField }}</td>
        <td>{{ studiengangField }}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup lang="ts">
import {ref, onMounted} from 'vue'
import type {Ref} from 'vue'

defineProps<{
  title: string
}>()

type Benutzer = { id?: number, nachname: string, vorname: string, studiengang: string }

const items: Ref<Benutzer[]> = ref([])
const nachnameField = ref('')
const vornameField = ref('')
const studiengangField = ('')

function loadUsers () {
  const endpoint ='http://localhost:8080/users'
  const requestOptions: RequestInit = {
    method: 'GET',
    redirect: 'follow',
  }
  fetch(endpoint, requestOptions)
      .then(response => response.json())
      .then(result => result.forEach((thing: Benutzer) => {
        items.value.push(thing)
      }))
      .catch(error => console.log('error', error))
}

function save () {
  const endpoint ='http://localhost:8080/users'
  const data: Benutzer = {
    nachname: nachnameField.value,
    vorname: vornameField.value,
    studiengang: studiengangField.valueOf()
  }
  const requestOptions: RequestInit = {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(data)
  }
  fetch(endpoint, requestOptions)
      .then(response => response.json())
      .then(data => {
        console.log('Success:', data)
      })
      .catch(error => console.log('error', error))
}

// Lifecycle hooks
onMounted(() => {
  loadUsers()
})
</script>

<style scoped>
h3 {
  text-align: center;
}
table {
  margin-left: auto;
  margin-right: auto;
}
button {
  color: blue;
}
</style>