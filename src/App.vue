<script setup>
    import { ref, reactive, onMounted } from 'vue'
    import { db } from './data/guitarra';
    import Guitar from './components/Guitar.vue';
    import Header from './components/Header.vue';
import Footer from './components/Footer.vue';

    const guitars = ref([])
     
    const cart = ref([])

    onMounted(() => {
        guitars.value = db
    })
     
    const addToCard = (guitar) =>{
        guitar.cantidad = 1;
        cart.value.push(guitar)
    }

</script>

<template>

    <Header 
        :guitar="guitars"
        :cart="cart"
        @add-to-Card="addToCard"
        
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
