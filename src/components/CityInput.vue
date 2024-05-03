<template>
    <div class="city-inner">
    <input
        type="text" 
        class="search" 
        placeholder="City name"
        :value="cityValueState"       
        @input="inputHandler"               
    >
    </div>
    <div v-if="options.length !== 0" class="dropdown">
        <div
            v-for="item in options"
            :key="item.id"
            :id="item.id"
            class="item"            
            @click="chooseCityHandler"
        >
            <p class="city">{{ item.name  }}</p>
            <p class="country">{{ item.country }}</p>
        
        </div>
    </div>

</template>

<script>
import { inject} from 'vue';

export default {
    setup(){
        const { cityValueState, updateCityValueState } = inject('cityValueKey');

        return {
            cityValueState,
            updateCityValueState,
        }
    },
    props: {
        options: {
            type: Array,
            default: []
        },
        callback: Function,
        chooseCityCallback: Function
    },
    methods: {
        inputHandler(event){
            const value = event.target.value
            if(value.length >= 3){
                this.callback(value)
            }
        },
        chooseCityHandler(e){
           const cityName = this.chooseCityCallback(e.currentTarget.id)
           console.log('user choose', cityName)
           this.updateCityValueState(cityName)
        }
    },
   
}
</script>

<style lang="sass" scoped>
@import '../assets/styles/main'

.city-inner
  position: relative
  display: inline-block
  width: 100%

.search
  width: 100%
  padding: 16px
  font-family: 'Inter', Arial, sans-serif
  color: $white
  background-color: rgba(56, 57, 118, 0.75)
  border-radius: 16px
  border: none
  outline: none
  cursor: pointer

.dropdown
    display: flex
    flex-direction: column
    row-gap: 5px
    position: absolute
    top: 120px
    width: 100%   
    z-index:10
    background: url('/src/assets/img/gradient-2.jpg') no-repeat 50% 50%
    background-size: cover
    border-radius: 8px
    padding: 10px

.item 
    display: flex
    align-items: center
    column-gap: 10px

.city
    padding:0
    margin: 0
    font-size: 18px

.country 
    padding:0
    margin: 0
    font-size: 14px
    font-style: italic 
    color: gray


</style>