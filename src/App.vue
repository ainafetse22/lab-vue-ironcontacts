<template>
  <div>
    <!-- <Button :showList="showList" :range="range"></Button> -->
    <button v-on:click="sortByName">Sort by name</button>
    <button v-on:click="sortByPopularity">Sort by popularity</button>
    <button v-on:click="addRandom">Add Random Contact</button>
    <ShowContacts :getContact="showList" @deleteContact="deleteContact"></ShowContacts>
  </div>
</template>

<script setup>
import contactsjson from "./contacts.json";
import {computed, ref, reactive} from 'vue'
import ShowContacts from "./components/ShowContacts.vue";
import Button from "./components/Button.vue";


const getContact = computed({
get: () => {
    let index=0;
    const formatContacts=reactive (contactsjson.map(contact=>{
        const contacts=[{}]
        index ++;
        contacts.index= index;
        contacts.id=contact.id;
        contacts.name=contact.name,
        contacts.picture= contact.pictureUrl,
        contacts.popularity= contact.popularity.toFixed([2]),
        contacts.oscar=contact.wonOscar,
        contacts.emmy= contact.wonEmmy
        return contacts;
        }))
    // const ContactList= formatContacts.slice(0,5);
    return formatContacts;
    }
}); 

function sortByName (){
  showList.value.sort((a,b)=> a.name > b.name ? 1 : -1);
  console.log(showList);
}

function sortByPopularity (){
  showList.value.sort((a,b)=> a.popularity < b.popularity ? 1 : -1);
  console.log(showList);
}
function deleteContact(elementToDelete){
  const indexToDelete = showList.value.findIndex(item => item.id === elementToDelete);
  showList.value.splice(indexToDelete,1);
}

function generateRandom(min,max) {
    // find diff
    let difference = max - min;
    // generate random number 
    let rand = Math.random();
    // multiply with difference 
    rand = Math.floor( rand * difference);
    // add with min value 
    rand = rand + min;
return rand;
}

function addRandom(){
    let isRepeat =false;
    let randomNumb;
    do{isRepeat =false;
        randomNumb = generateRandom(0,range.value);  
        showList.value.forEach(element => {
            if(element.index===randomNumb)
                isRepeat=true;
        })
       
    }
    while(isRepeat===true);
    const newElement = getContact.value.find(elemen=> elemen.index===randomNumb);
    showList.value.push(newElement);
    console.log(showList)
    console.log(newElement);
    console.log(showList)
    // return randomNumb;    
}

const range= ref(getContact.value.length);
// const showList= getContact.value.slice(0,5);  
const showList= ref([]);
for(let i=0;i<5;i++){
  showList.value.push(getContact.value.shift());
}
// const showListIndex= showList.map.index()
</script>


<style>
</style>
