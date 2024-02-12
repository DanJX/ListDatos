<script setup lang="ts">
import { ref } from 'vue';
import PersonajeList from './components/Personajes/PersonajeList.vue';
import PersonajeData from './data/PersonajesData';
import type { IPersonaje } from './interfaces/IPersonaje';
import FormView from './views/FormView.vue';

const addData = (event: IPersonaje) => {
  key.value += 1
  PersonajeData.push(event)
}

const key = ref(0);

</script>

<template>
  <main>
    <section class="container">
      <div class="pad">
        <h1 class="txt-center">Registro</h1>
        <FormView @-card-pers="addData($event)"/>
      </div>
      <div class="pad">
        <h1 class="txt-center">Items</h1>
        <PersonajeList :key="key"/>
      </div>
    </section>
  </main>
</template>

<style scoped>

.pad{
  padding-right: 30px;
}
.container{
  display: flex;
}
.txt-center{
  text-align: center;
  margin-bottom: 15px;
  background: white;
  color: black;
  font-weight: bold;
  text-transform: uppercase;
  border-radius: 10px;
}
</style>
./data/PersonajeData./interfaces/IPersonaje