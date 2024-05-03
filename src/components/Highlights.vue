<script setup>
import Card from './Card.vue'

</script>

<script>
export default {
  props: {
    temperatures: Array,    
  }, 
  
}
</script>

<template>
    <div class="section highlights">
        <h3 class="title">
          Highlights
        </h3>
        <div class="cards">
          
        <Card
          v-for="item in temperatures"
          :key="item.date"
          :date="item.date"
          :temperature="item.temperature"
         /> 
        </div>
      </div>

</template>

<style lang="sass" scoped>
@import '../assets/styles/main'

.cards
    display: flex
    column-gap: 10px    

.title
  padding-bottom: 5px
  font-size: 18px 

</style>