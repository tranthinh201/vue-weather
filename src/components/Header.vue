<template>
    <header class="flex justify-around items-center p-10" >
        <div class="flex">
            <div class="mr-4">
                <img src="../assets/logo.png" alt="logo" class="w-10 overflow-hidden">
            </div>
            <div class="mx-2">
                <p class=""><b>HELLO,</b></p>
                <p>Tran Thinh</p>
            </div>
        </div>

        <div class="flex items-center mx-2">
            <form @submit.prevent="sendCity" class="flex relative mr-2">
                <input 
                    type="text"
                    v-model="city"
                    placeholder="Nhập tên thành phố..." 
                    class="outline-none border px-4 py-2 rounded-[6px]"
                >
                <button class="absolute top-2/1 right-1 translate-y-1/2 outline-none" type="submit">
                    <img 
                        class="" 
                        src="../assets/icons/search.png" 
                        alt="image"
                    >
                </button>
            </form>
            <div class="ml-2 border-solid border rounded-full p-2.5 border-gray-100">
                <img src="../assets/icons/bell.png" alt="image" class="w-6">
            </div>
        </div>
    </header>
</template>


<script>
import { ref } from '@vue/reactivity'
    export default {
        setup(props, context) {
            const city = ref('')

            const sendCity = () => {
                context.emit('name-city', city.value)
            }

            return {
                city,
                sendCity
            }
        }
    }
</script>

<style scoped>

</style>