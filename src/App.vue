<template>
  <div>
    <ShowContacts :getContact="getContact"></ShowContacts>
  </div>
</template>

<script setup>
  import contactsjson from "./contacts.json";
  import {computed, ref} from 'vue'
import ShowContacts from "./components/ShowContacts.vue";

const getContact = computed({
    get: () => {    
        const contacts = contactsjson.map((contact=> {
           return {name:contact.name,
            picture: contact.pictureUrl,
            popularity: contact.popularity
            }
        }));
          //contactsjson.slice(0,4);

    return contacts;
  }

})
   
</script>


<style>
</style>
