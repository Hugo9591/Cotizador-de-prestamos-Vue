<!-- //----------------------------sintaxis de Composition API -->
<script setup>
  import Header from './components/Header.vue';
  import Button from './components/Button.vue';
  import {ref, reactive, computed, watch} from 'vue'
  import { calcularTotalPagar } from './helpers';

//Definir state
  //ref
  const cantidad = ref(10000);
  const meses = ref(6);
  const total = ref(0);
  //console.log(cantidad.value);

  //reactive
  //const state = reactive({cantidad: 0});
  //console.log(state.cantidad);

  const MIN = 0;
  const MAX = 20000;
  const STEP = 100;

  // ya no es necesario esta funcion por el v-model
  //function handleChange(e){
    //modificar ref
    //cantidad.value = +e.target.value;

    //modificar reactive
    //state.cantidad = +e.target.value;
  //}


  //Computed Properties - Formato al dinero
 
  const formatearDinero = (valor) => {
    const formatter = new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD'
    });

    return formatter.format(valor);
  };

  //cada vezque cambie cantidad o/y mesesse ejecuta el callback
  watch([cantidad, meses], () =>{
    //modificar el total
    total.value = calcularTotalPagar(cantidad.value, meses.value);
  }, {immediate: true});//calcula el codigo al instante en este caso el total

  const pagoMensual = computed(() => {
    return total.value / meses.value;
  });


  const handleChangeDecremento = () => {
    const valor = cantidad.value - STEP;

    if(valor < MIN){
      alert('Cantidad no Valida');
      return;
    }

    cantidad.value = valor;
  }

  const handleChangeIncremento = () => {
    const valor = cantidad.value + STEP;

    if(valor > MAX){
      alert('Cantidad no Valida');
      return;
    }

    cantidad.value = valor;
  }
</script>

<!-- -----------------------------------Sintaxis Option API -->
 <!-- <script>
  import Header from './components/Header.vue';

  export default {
    components: {
      Header
    }
  }
</script> -->

<template>
  <div class="my-20 max-w-lg mx-auto bg-white shadow p-10">
    <Header />

    <div class="flex justify-between my-6">
      <!-- cuando hay un : son props y cuando hay @ sson eventos personalizados -->
     <Button 
        :operador="'-'"
        @funcion="handleChangeDecremento"/>

     <Button 
        :operador="'+'"
        @funcion="handleChangeIncremento"/>

    </div>

    <input 
        type="range" 
        class="w-full bg-gray-200 accent-lime-500 hover:accent-lime-600"
        :min="MIN"
        :max="MAX"
        :step="STEP"
        v-model.number="cantidad"
      />
      <!-- con el v-model es lo mismo que tener la funcion handleChanage -->
  
      <!--imprimir state -->
    <p class="text-center my-10 text-5xl font-extrabold text-indigo-600">{{ formatearDinero(cantidad) }}</p>
    <!-- <p v-text="cantidad"></p> -->

    <h2 class='text-2xl font-extrabold text-gray-500 text-center'>
        Elige un <span class='text-indigo-600'>Plazo</span> a pagar.
    </h2>

    <select class='mt-5 w-full p-2 bg-white border border-gray-300 rounded-lg text-center text-xl font-bold text-gray-500'
            :value="meses"
            v-model.number="meses">
        <option value="6">6 Meses</option>
        <option value="12">12 Meses</option>
        <option value="24">24 Meses</option>
    </select>

    <!-- space-y-3: les da un padding a cada uno de sus hijos -->
     <!-- v-if calcula el total cuando este sea mayor a cero -->
    <div v-if="total > 0" class='my-5 space-y-3 bg-gray-50 p-5'>
        <h2 class='text-2xl font-extrabold text-gray-500 text-center'>
          Resumen <span class='text-indigo-600'>de Pagos</span>
        </h2>

        <p class='text-xl text-gray-500 text-center font-bold'>{{ meses }} Meses</p>
        <p class='text-xl text-gray-500 text-center font-bold'>Total a Pagar: {{formatearDinero(total) }} </p>
        <p class='text-xl text-gray-500 text-center font-bold'> Mensuales: {{ formatearDinero(pagoMensual) }}</p>
    </div>
    
    <p v-else class="text-xl text-gray-400 text-center font-bold pt-6">Añade una cantidad </p>
  </div>

  
</template>
