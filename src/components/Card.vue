<script setup>
import moment from 'moment';
</script>

<template>
    <article class="card">        
        <p class="card-text">{{temperature}}</p>
        <div class="date text-block">
       {{moment(date, "YYYY-MM-DD[T]hh[:]mm").format('LL')}}
      </div>    
    </article>
</template>

<script >

export default {
    props: {
        date: String,
        temperature: String
    }
}
</script>

<style lang="sass" scoped>
@import '../assets/styles/main'

.card
  display: flex
  flex-direction: column
  justify-content: center
  min-height: 30px
  padding: 10px
  background: url('/src/assets/img/gradient-2.jpg') no-repeat 50% 50%
  background-size: cover
  border-radius: 8px
  width: 140px

  &-text   
    display: flex
    justify-content: center   
    font-size: 26px


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
    
.date

 &::before
  left: 2px
  width: 15px
  height: 15px
  background-image: url('/src/assets/img/calendar.svg')

</style>