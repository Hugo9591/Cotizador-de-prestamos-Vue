<script setup>
    //Hay 2 formas de leer los props

    //array
    //const props = defineProps(['operador','funcion']);

    //Objeto
    //conts props = defineProps({operador: String, funcion: Function});

    const props = defineProps(['operador']);


</script>

<template>
    <!-- emit se usa para comunicarte con eventos personalizados -->
    <button
        type="button"
        className="h-10 w-10 flex items-center justify-center font-bold text-white text-2xl bg-lime-500 rounded-full
        hover:outline-none hover:ring-2 hover:ring-offset-2 hover:ring-lime-500"
        @click="$emit('funcion')"
        >{{ operador }}
    </button>
</template>