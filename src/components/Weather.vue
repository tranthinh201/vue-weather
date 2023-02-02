<template>
    <div class="flex">
        <div class="bg-blue-100 bg-image p-4">
            <div class="flex items-center justify-start">
                <div class="flex bg-white-300 mr-4">
                    <img src="../assets/icons/sun.png" alt="icon" class="w-8">
                </div>
                <div>
                    <p class="text-lg font-semibold ">Weather in {{ nameCity }}</p>
                    <p>What's the weather?</p>
                </div>
            </div>
            <h1 class="font-bold text-2xl">{{ temp }} °C</h1>
            <div class="flex">
                <img src="https://openweathermap.org/img/wn/01n.png" alt="icon" class="icon" />
                <div class="description">Sunny</div>
            </div>
            <div class="humidity">Humidity: 60%</div>
            <div class="wind">Wind speed: 1000km/h</div>
        </div>
    </div>
</template>

<script>
import { ref } from '@vue/reactivity'
    export default {
        props: {
            data: Array 
        },
        setup(props, context) {
            const nameCity = ref('')
            const temp = ref('')
            console.log(props.data)
            nameCity.value = props?.data?.name
            temp.value = props?.data?.main?.temp
            return {
                nameCity,
                temp
            }
        }
    }
</script>

<style scoped>
    .bg-image {
        background: url('../assets/icons/sunset.png');
        background-repeat: no-repeat;
    }
</style>
