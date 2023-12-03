<script setup lang="ts">

</script>

<template>
  <div class="row row-cols-1 row-cols-md-3 g-4">
    <div class="col">
      <div class="card h-100">
        <img src="..." class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">Card title</h5>
          <p class="card-text">This is a wider card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
        </div>
        <div class="card-footer">
          <small class="text-body-secondary">Last updated 3 mins ago</small>
        </div>
      </div>
    </div>
    <div class="col">
      <div class="card h-100">
        <img src="..." class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">Card title</h5>
          <p class="card-text">This card has supporting text below as a natural lead-in to additional content.</p>
        </div>
        <div class="card-footer">
          <small class="text-body-secondary">Last updated 3 mins ago</small>
        </div>
      </div>
    </div>
    <div class="col">
      <div class="card h-100">
        <img src="..." class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">Card title</h5>
          <p class="card-text">This is a wider card with supporting text below as a natural lead-in to additional content. This card has even longer content than the first to show that equal height action.</p>
        </div>
        <div class="card-footer">
          <small class="text-body-secondary">Last updated 3 mins ago</small>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default{
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'User',
  data (){
    return{
      users:[
        {
          id: 1,
          nachname: 'Nguyen',
          vorname: 'Hoang',
          studiengang: 'Wirtschaftsinformatik'
        },
        {
          id: 2,
          nachname: 'Nothelfer',
          vorname: 'Daniel',
          studiengang: 'Wirtschaftsinformatik'
        }
      ]
    }
  },
  methods: {
    loadUsers(){
      const endpoint = 'http://localhost:8080'
      const requestOptions = {
        method: 'GET',
        redirect: 'follow'
      }
      fetch(endpoint, requestOptions)
          .then(response => response.json())
          .then(result => result.forEach(user => {this.items.push(user)
          }))
          .catch(error => console.log('error', error))
    }
  }
}
</script>

<style scoped>

</style>