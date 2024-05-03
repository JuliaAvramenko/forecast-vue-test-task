<script setup>
import WeatherSummary from './WeatherSummary.vue'
import Highlights from './Highlights.vue'
import CityInput from './CityInput.vue';
import moment from 'moment';
import { provide, ref } from 'vue';


const cityValueState = ref('');
const updateCityValueState = (newValue) => {
    console.log('i change value',cityValueState.value, newValue )
    cityValueState.value = newValue
};
provide('cityValueKey', {
    cityValueState,
    updateCityValueState,
});

</script>

<template>
     <div class="sections">
        <h2 class="title">Daily Weather Forecast</h2>
        
            <CityInput
                :options="cities"
                :callback="searchCoordinates"
                :chooseCityCallback="getWeather"
            />

            <WeatherSummary
                v-if="forecastDaily.length > 0"
                :temperature="forecastDaily[0].temperature"
                :date="forecastDaily[0].date"
                :city="cityValueState"
                :country="inputCountry"
            />           
      
        <Highlights
            v-if="forecastDaily.length > 1"
            :temperatures='forecastDaily.slice(1)'
            />
    </div>
</template>

<script>
export default {
    setup() {

    },
    methods: {
        searchCoordinates(city){
            let queryParams = {
                name: city,
                count: 10,
                language: 'en',
                format: 'json'
            }
            queryParams = new URLSearchParams(queryParams)
            fetch(`https://geocoding-api.open-meteo.com/v1/search?${queryParams.toString()}`)
                .then((response)=> response.json())
                .then((data)=>{
                                     
                    this.cities = data.results && data.results.map((item)=>{
                        return {
                            id: item.id, 
                            longitude: item.longitude,
                            latitude: item.latitude,
                            name: item.name,
                            country: item.country
                        }
                    }) || []
                })
        },
        getWeather(cityId) {
            

            const city = this.cities.filter(item => item.id === Number(cityId))[0]
            this.inputCountry = city.country
            this.cities = []

            const now = moment()
            const fromDate =  now.format('YYYY-MM-DD')
            const toDate = moment().add(4, 'days').format('YYYY-MM-DD')


        
            let queryParams = {
                latitude: city.latitude,
                longitude: city.longitude,
                hourly: 'temperature_2m',
                start_date: fromDate,
                end_date: toDate
            }
            queryParams = new URLSearchParams(queryParams)

            fetch(`https://api.open-meteo.com/v1/forecast?${queryParams.toString()}`)
            .then((response)=> response.json())
            .then((data) => {
                const forecastDaysArray = data.hourly.time.reduce((acc, item, index)=>{
                    if(item.endsWith('T12:00')){
                        acc.push({
                            day: item,
                            index
                        })
                    }

                    return acc
                },[])
                this.forecastDaily = forecastDaysArray.map(item => {
                    return {
                        date: item.day,
                        temperature: `${Math.round(data.hourly.temperature_2m[item.index])} ${data.hourly_units.temperature_2m}`

                    }
                })
                
            }) 

            return city.name
        }
    },
    data() {
        return {
            cities: [],
            inputCountry: '',
            forecastDaily: []
        }
    },
}
</script>

<style lang="sass" scoped>
@import '../assets/styles/main'

.sections
  display: flex
  flex-direction: column
  width: 100%
  position: relative

.title
    font-size: 25px  
    


</style>
