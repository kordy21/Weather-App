<template>
    <div>

    </div>
</template>

<script setup>
    import axios from 'axios';
    import { useRoute } from 'vue-router';
    
    const route =useRoute();
    const getWeatherData = async ()=>{
        try{
            const weatherData =await axios.get(`https://api.openweathermap.org/data/3.0/onecall?lat=${route.query.lat}&lon=${route.query.lng}&exclude={part}&appid=604b9d0787b2de1b232f419af00f0494&units=imperial`);

            // cal current data & time 
            const localOffset = new Data().getTimezoneOffset() * 60000;
            const utc = weatherData.data.current.dt * 1000 + localOffset;
            weatherData.data.currentTime = utc + 1000 * weatherData.data.timezone_offset;

            // cal hourly weather offset
            weatherData.data.hourly.foreach((hour) => {
                const utc =hour.dt * 1000 + localOffset;
                hour.currentTime = utc + 1000 * weatherData.data.timezone_offset;
            }) ;
            return weatherData;
        }catch (err){
            console.log(err)
        }
    };
    const weatherData =await getWeatherData();
    console.log(weatherData);
</script>

