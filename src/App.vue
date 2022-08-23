<template>
<h2> profile count: {{profiles.length}}</h2>

<input type="text" v-model.trim="id"> {{id}}
<br>

<input type="text" placeholder="username" v-model="formValues.username">
<input type="text" placeholder="email" v-model="formValues.email">
<input type="text" placeholder="ImageUrl" v-model="formValues.imageUrl">


<br>
<button @click="insertDoc"> Insert student </button>

<button @click="updateDoc"> Update students details </button>

<button @click="getDoc"> Get students details </button>

<button @click="deleteDoc"> Delete students details </button>

<br>



<ul>
  <li v-for="profile in profiles">
  <img :src="profile.imageUrl" alt="" width="50">
  {{profile.imageUrl}}
   {"id is here" {{profile._id}} }
  {{profile.username}}
  {{profile.email}}
  </li>
</ul>



</template>


<script>
const api ="https://rest-api-express-mongodb.netlify.app/.netlify/functions/api/"
// const api = "https://rest-api-jameseddievictoria.netlify.app/.netlify/functions/api/"
export default{
  data(){
    return{
  profiles: [],
  id: "",
  formValues: {
username: "",
email: "",
imageUrl: "",
  }
 }
},
methods:{
  //Post aka insert the item
  insertDoc(){
    fetch(api, {
      method:"POST",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify(this.formValues)
      })
  .then((response) => response.text())
  .then((data) => {
    console.log(data)
  })
  .catch((err) => {
    if (err) throw err;
  })
  },


   //Put aka update the item
  updateDoc(){
    fetch(api + this.id, {
      method:"PUT",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify(this.formValues)
      })
  .then((response) => response.text())
  .then((data) => {
    console.log(data)
  })
  .catch((err) => {
    if (err) throw err;
  })
  },

  //Get fetch aka find the item
  getDoc(){
    fetch(api + this.id, {
      method:"GET",
     
      })
  .then((response) => response.json())
  .then((data) => {
    console.log(data)
  })
  .catch((err) => {
    if (err) throw err;
  })
  },

 //Delete the item
  deleteDoc(){
    fetch(api + this.id, {
      method:"DELETE",
      })

  .then((response) => response.text())
  .then((data) => {
    console.log(data)
  })
  .catch((err) => {
    if (err) throw err;
  })
  }


},

mounted(){
  fetch(api)
  .then((response) => response.json())
  .then((data) => {
    this.profiles = data
  })
  .catch((err) => {
    if (err) throw err;
  })

}
}
</script>


<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
