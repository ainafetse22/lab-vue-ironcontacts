<template>
<table class="table">
              <thead></thead>
              <tbody>
                <tr>
                  <td >Picture</td>
                  <td>Name</td>
                  <td>Popularity</td>  
                </tr>
                <tr v-for="n in 5" :key="getContact[n].id">
                  <td><img :src="getContact[n].picture"/></td>
                  <td>{{getContact[n].name}}</td>
                  <td>{{getContact[n].popularity}}</td>
                </tr>
              </tbody>
            </table>  
</template>

<script setup>
import {defineProps, ref} from 'vue'
const props= defineProps({
    getContact:Array
})

</script>

<style>

</style>