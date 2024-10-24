<script setup>
    import { ref, reactive, onMounted } from 'vue'
    import { db } from './data/guitarra';
    import Guitar from './components/Guitar.vue';
    import Header from './components/Header.vue';

    const guitars = ref([])
     
    const cart = ref([])

    onMounted(() => {
        guitars.value = db
    })
    
    const addToCard = (guitar) =>{
        guitar.cantidad = 1;
        cart.value.push(guitar)
        console.log('this data',cart.value)
    }

</script>

<template>

    <Header 
        :guitar="guitars"
        :cart="cart"
        
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


    <footer class="bg-dark mt-5 py-5">
        <div class="container-xl">
            <p class="text-white text-center fs-4 mt-4 m-md-0">GuitarLA - Todos los derechos Reservados</p>
        </div>
    </footer>

</template>

<style scoped>

</style>
