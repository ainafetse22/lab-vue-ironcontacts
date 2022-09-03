<template>
<table class="table">
              <thead>
                <tr>
                  <td >Picture</td>
                  <td>Name</td>
                  <td>Popularity</td>  
                  <td>Won Oscar</td>
                  <td>Won Emmy</td>
                  <td></td>
                </tr>
            </thead>
                <tbody v-if="getContact.length">
                <tr v-for="contact in getContact" :key="contact.id">
                  <td><img :src="contact.picture"/></td>
                  <td>{{contact.name}}</td>
                  <td>{{contact.popularity}}</td>
                  <td v-show="contact.oscar"><img src="https://cdn-icons-png.flaticon.com/512/3254/3254738.png"/></td>
                  <td v-show="contact.emmy"><img src="https://cdn-icons-png.flaticon.com/512/3254/3254738.png"/></td>
                  <td><button v-on:click="deleteButton(contact.id)">Delete</button></td>
                </tr>
              </tbody>
            </table>  
</template>

<script setup>
import {defineProps, ref, defineEmits} from 'vue'
const props= defineProps({
    getContact:Array
})
const emit = defineEmits(['deleteContact']);
function deleteButton(contacId){
   
 emit('deleteContact',contacId);
//     const emit = defineEmits(['deleteContact'])
//   emit(deleteContact,contactId)
}

</script>

<style>

</style>