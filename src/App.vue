<template>
 <div class="container">
        <h1 class="contacts">Iron contacts</h1>
    <div class="buttons">
      <button @click="addContact">Add Random Contact</button>
      <button @click="sortbyPopularity">Sort By Popularity</button>
      <button @click="sortbyName">Sort By Name</button>
    </div>
        <table class="table-contacts">       
                <tr>
                    <th>Picture</th>
                    <th>Name</th>
                    <th>Popularity</th>
                    <th>won Oscar</th>
                    <th>won Emy</th>
            
                </tr>
                 <tr v-for="contact in initialContacts" :key="contact.name">
                    <td><img :src="contact.pictureUrl" :alt="contact.name"></td>
                    <td>{{contact.name}}</td>
                    <td>{{contact.popularity.toFixed(2)}}</td>
                    <td>{{contact.wonOscar ? "🏆" :" "}}</td>
                    <td>{{contact.wonEmmy ? "🏆" :" "}}</td>
                    <td><button @click="deleteContact(contact)">Delete</button></td>
                 </tr>
        </table>
        <div>
            
        </div>
    </div>    
</template>

<script setup>
import contacts from "./contacts.json";
import { reactive } from "vue";
const myContacts = reactive(contacts);
console.log(myContacts);
const initialContacts = reactive(contacts.slice(0,5));
console.log(initialContacts);
const remainingContacts = reactive(contacts.slice(5));
console.log(remainingContacts)

function addContact() {
  const randomNum = Math.floor(Math.random() * remainingContacts.length);
  // pick a random actor from the remaining list
  initialContacts.push(remainingContacts[randomNum]); // add actor to the initial list
  remainingContacts.splice(randomNum, 1); // remove actor from the remaining list
}
function sortbyPopularity() {
  initialContacts.sort((a, b) => (a.popularity < b.popularity ? 1 : -1));
}
function sortbyName() {
  initialContacts.sort((a, b) => (a.name > b.name ? 1 : -1));
}
function deleteContact(contact) {
  const index = initialContacts.indexOf(contact);
  initialContacts.splice(index, 1);
}

</script>

<style>
.container{
  text-align: center;
  margin: 40px;
  font-size: large;
  background-color: #f1eae1;
  color:  rgb(59, 52, 52);
  }
.table-contacts{
 width:100%;
}
.contacts{
 padding: 10px;
}
img{
  width: 5em;
}
  button{
    margin: 50px;
  }
 
</style>
