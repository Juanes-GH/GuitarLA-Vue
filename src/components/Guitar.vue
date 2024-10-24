<script setup>
import { ref } from 'vue';

    const props = defineProps({
        guitar:{
            type: Object,
            requited: true
        }
    })

    defineEmits(['add-to-Card'])
</script>

<template>
    <div class="col-md-6 col-lg-4 my-4 row align-items-center">
        <div class="col-4">
            <img 
                class="img-fluid" 
                :src="'./public/img/' + guitar.imagen + '.jpg'" :alt="'guitar image '+ guitar.nombre">
        </div>
        <div class="col-8">
            <h3 class="text-black fs-4 fw-bold text-uppercase">{{ guitar.nombre }}</h3>
            <p>{{ guitar.descripcion }}</p>
            <p class="fw-black text-primary fs-3">${{ guitar.precio }}</p>
            <button 
                type="button"
                class="btn btn-dark w-100"
                @click="$emit('add-to-Card', guitar)"
            >
                Agregar al Carrito
            </button>
        </div>
    </div>
</template>


<style>

</style>