<template>

<div id="header">

  <h1>Protégé</h1>
<h3> profile count: {{profiles.length}}</h3>

<input type="text" v-model.trim="id"> 
<!-- {{id}} --> 
<br>
<br>

<input type="text" placeholder="username" v-model="formValues.username">
<input type="text" placeholder="email" v-model="formValues.email">
<input type="text" placeholder="ImageUrl" v-model="formValues.imageUrl">


<br>
<br>
<button @click="insertDoc"> Insert student </button>

<button @click="updateDoc"> Update students details </button>

<button @click="getDoc"> Get students details </button>

<button @click="deleteDoc"> Delete students details </button>

<br>

</div>

<ul>
  <li v-for="profile in profiles" id="flex-cont">
  <img :src="profile.imageUrl" alt="" width="50">
<br>
  id# {{profile._id}} 
  <br>
  User name: {{profile.username}}
  <br>
  Email: {{profile.email}}
  <hr>
  </li>
</ul>

<hr>


</template>


<script>
// const api ="https://rest-api-express-mongodb.netlify.app/.netlify/functions/api/"
const api = "https://rest-api-jameseddievictoria.netlify.app/.netlify/functions/api/"

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


 body {
        font-family: 'Roboto', sans-serif;
        text-align: center;   
    }
 
    #headertext {
        display: flex;
        flex-direction: column;
    }
    #logoimg {
        width: 250px;
        height: auto;
        margin: 20px;
    }
    #headertext {
        margin-right: 20px;
        margin-bottom: 0px;
        justify-content: center;
    }
   
img{border-radius: 50%;
height: 10vw;
width: 10vw;
margin-right: 5vw;}

#flex-cont{
  display: flex;
  flex-direction: row;
  align-items: center;
  align-content: space-between;
}



li{
  padding-top: 20px;
}


   * {
        font-family: Roboto, sans-serif;
        margin: 0;
    }
    #header {
        background-image: linear-gradient(#36C5C8, #3192D1);
        height: 30%;
        width: 100%;
        margin: auto 0;
        padding: 20px;
    }
  
    p {
        line-height: 1.3rem;
    }
    h1 {
        font-size: 100px;
        font-weight: 900;
        margin: 0;
        color: white;
    }
    h2 {
        font-size: 40px;
        font-style: italic;
        margin: 0;
        color: white;
    }
    h3 {
        font-weight: 700;
        font-size: 1.4rem;
        margin: 10px 0 20px 0;
        color: white;
    }
input{border: none;
        padding: 6px 10px;
        background-color: #a5a5a5;
        border-radius: 20px;
          font-weight: 600;
        font-size: 0.8rem;
        margin: 10px;
        color: #ffffff;}


button {
        border: rgb(255, 255, 255) solid 2px;
        padding: 6px 10px;
        background-color: #3192D1;
        border-radius: 20px;
        color: #ffffff;
        font-weight: 600;
        font-size: 0.8rem;
        margin: 10px;
    }
    button:hover {
        background-color: #ffffff;
        color: #3192D1;
        border: rgb(255, 255, 255) solid 2px;
    }

</style>
