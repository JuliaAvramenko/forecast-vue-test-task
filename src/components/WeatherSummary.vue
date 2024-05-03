<script setup>
import moment from 'moment';
</script>

<template>
  <div class="summary">
                    
    <div class="weather temp">
      {{ temperature }}
    </div>
    <div class="location">
      <div class="city text-block">
        {{ city }},
        {{ country }}
      </div>
      <div class="date text-block">
        {{moment(date, "YYYY-MM-DD[T]hh[:]mm").format('LL')}}
      </div>
    </div>
  </div>

</template>

<script>
export default {
  props: {
    temperature: String,
    date: String,
    city: String,
    country: String,

  }, 
  data() {

  }
}
</script>

<style lang="sass" scoped>
@import '../assets/styles/main'

.summary
  display: flex
  border-bottom: 1px solid rgba(255, 255, 255, 0.4)
  padding: 20px 0
  margin: 0 0 20px
  

.city
  font-size: 24px

.weather
  border-right: 1px solid rgba(255, 255, 255, 0.4) 
  padding-right: 10px
  
.location 
  padding-left:10px

.temp
  font-size: 32px

.text-block
  position: relative
  padding-left: 24px
  padding-bottom: 8px
  font-size: 12px

  &::before
    content: ''
    position: absolute
    top: 0
    left: 0
    width: 20px
    height: 20px
    margin-right: 6px
    background-repeat: no-repeat
    background-position: 50% 50%
    background-size: contain

.city

  &::before
    background-image: url('/src/assets/img/location.svg')

.date

  &::before
    left: 2px
    width: 15px
    height: 15px
    background-image: url('/src/assets/img/calendar.svg')

</style>