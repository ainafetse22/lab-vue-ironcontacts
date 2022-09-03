<template>
<div>
    <button v-on:click="addRandom">Add Random Contact</button>
    <h1>{{range}}</h1>
</div>  
</template>

<script setup>
import { defineProps,defineEmits } from 'vue';

const props= defineProps({
    showList:Array,
    range: Number
})


function addRandom(){
    let isRepeat =false;
    let randomNumb;
    do{isRepeat =false;
        randomNumb = generateRandom(0,props.range);  
        props.showList.forEach(element => {
            if(element.index===randomNumb)
                isRepeat=true;
        })
        console.log(randomNumb)
    }
    while(isRepeat===true);
    return randomNumb;    
}

const emit = defineEmits(['randomNumb']);
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
</script>

<style>

</style>