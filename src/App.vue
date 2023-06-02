<script setup>
  import { ref, computed } from 'vue';
  const contador = ref(0);
  const favoritos = ref([]);

  const increment = () => contador.value ++;

  const decrement = () => contador.value --;

  const reset = () => contador.value = 0;

  const fav = ()=> {
    if(contador.value != "" || contador.value === 0){
      favoritos.value.push(contador.value);
    }
  }

  const nofav = () =>{
    const index = favoritos.value.indexOf(contador.value);
    favoritos.value.splice(index, 1)
  }

  const repetido = computed(()=>{
    if(favoritos.value.includes(contador.value)){
      console.log("repetido");
      console.log(contador.value + 2);
      return 'true';
    }
  });

  const eliminar = computed(()=>{
    if(!(favoritos.value.includes(contador.value))){
      return true;
    }
  });

  const vaciar = () =>{
    favoritos.value = [];
  }

  const error = computed(()=>{
    if(contador.value === ""){
      return 'block';
    }
    return 'none';
  });

</script>

<template>
  <h1 class="display-2 text-center m-3">Contador</h1>
  <div class="card mx-auto m-4 w-75">
    <input class="mx-auto text-center display-2 w-25 border" onkeypress='return event.charCode>=48 && event.charCode<=57' type="number"  :value="contador" @input="(e)=>contador = Number(e.target.value)" required >
    <p class="text-center mx-auto m-1 text-danger" :style="`display:${error}`">Atencion rellenar el campo</p>
    <div class="d-flex justify-content-center">
      <button class="btn bg-danger bg-gradient m-1 fs-4 text" @click="decrement">Disminuir (-1)</button>
      <button class="btn bg-success bg-gradient m-1 fs-4 text" @click="increment">Incrementar (+1)</button>
      <button class="btn bg-warning bg-gradient m-1 fs-4 text" @click="reset">Reset (0)</button>
      <button :disabled="repetido" class="btn bg-primary bg-gradient m-1 fs-4 text" @click="fav">Favorito 🌟</button>
      <button :disabled="eliminar" class="btn bg-primary bg-gradient m-1 fs-4 text" @click="nofav">Eliminar de favoritos ❌</button>
    </div>
  </div>

  <div class="card w-75 mx-auto">
    <h2 class="display-6 m-2 text-center">Números favoritos</h2>
    <div class="text-center">
    <span class="display-7 text-center m-3 fs-2" v-for="fav, index in favoritos" :key="index">{{ fav }}</span>
    </div>
    <button class="bg-danger fs-5" @click="vaciar">Eliminar todos los números favoritos</button>
  </div>
</template>

<style>

  @media (max-width: 660px){
    .d-flex{
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    .d-flex button{
      width: 70%;
      margin: 0.5rem 1rem;
    }
  }

</style>
