<script setup>
import { ref, reactive, onMounted } from 'vue'
import { db } from './data/guitarra';
import Guitar from './components/Guitar.vue';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';
    const guitars = ref([])
    const cart = ref([])
    const guitar = ref({})
    onMounted(() => {
        guitars.value = db
        guitar.value = db[3]
    })
    const addToCard = (guitar) =>{
        const guitarExist = cart.value.findIndex( product => product.id === guitar.id)
        if(guitarExist >= 0){
            cart.value[guitarExist].stock++
        }else{
            guitar.stock = 1;
            cart.value.push(guitar)
        }
    }
    const decreaseQuantity = (id) =>{
        const index = cart.value.findIndex( product => product.id === id)
        
        if (cart.value[index].stock > 1) {
            cart.value[index].stock--;
        } else {
            cart.value.splice(index, 1);
        }
        
    }
    const increaseQuantity = (id) => {
        const index = cart.value.findIndex( product => product.id === id)
        if(cart.value[index].stock >= 10) return 
        cart.value[index].stock++
    }
    const deleteGuitar = (id) => {
        cart.value = cart.value.filter(gui => gui.id !== id);
    }

    const clearCart = () => {
        cart.value = []
    }
</script>
<template>
    <Header 
        :cart="cart"
        :guitar="guitar"
        @add-to-Card="addToCard"
        @decrease-quantity="decreaseQuantity"
        @increase-quantity="increaseQuantity"
        @clear-cart="clearCart"
        @delete-guitar="deleteGuitar"
    />
    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>
        <div class="row mt-5">
            <Guitar 
                v-for="guitar in guitars"
                :key="guitar.id"  
                :guitar = "guitar"
                @add-to-Card="addToCard"
            />
        </div>
    </main>
    <Footer />
</template>
<style scoped>
</style>
