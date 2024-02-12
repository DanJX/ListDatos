<script setup lang="ts">
import PersonajeData from '@/data/PersonajesData';
import { ref } from 'vue';
import type { Ref } from 'vue';
const nombre: Ref<string> = ref('');
const region: Ref<string> = ref('');
const otra_reg: Ref<string> = ref('');
const elemento: Ref<string> = ref('');
const otro_elem: Ref<string> = ref('');
const arma: Ref<string> = ref('');
const otra_arm: Ref<string> = ref('');
const rareza: Ref<string> = ref('');

const errores: any = ref([
]);
const emits = defineEmits(['CardPers']);

const validations = () => {
  limpiar();

  if (nombre.value.length < 8 || nombre.value.length > 30) {
    errores.value.push("Mínimo 8 carácteres y Máximo 30 en nombre");
  }
  if (region.value == 'otro' && (otra_reg.value.length < 8 || otra_reg.value.length > 30)) {
    errores.value.push("Mínimo 8 carácteres y Máximo 30 en región");
  }
  if (elemento.value == 'otro' && (otro_elem.value.length < 8 || otro_elem.value.length > 30)) {
    errores.value.push("Mínimo 8 carácteres y Máximo 30 en elemento");
  }
  if (arma.value == 'otro' && (otra_arm.value.length < 8 || otra_arm.value.length > 30)) {
    errores.value.push("Mínimo 8 carácteres y Máximo 30 en arma");
  }
}

const enviar = () => {
  limpiar();
  const personajes = PersonajeData.some(personaje => personaje.nombre == nombre.value)
  if (!personajes) {
    const id = PersonajeData.length + 1;
    emits('CardPers', {
      id: id,
      nombre: nombre.value,
      region: region.value == 'otro' ? otra_reg.value : region.value,
      elemento: elemento.value == 'otro' ? otro_elem.value : elemento.value,
      arma: arma.value == 'otro' ? otra_arm.value : arma.value,
      rareza: rareza.value
    })
  } else {
    errores.value.push("Ya existe este personaje");
  }
}

const limpiar = () => {
  errores.value = []
}
</script>

<template>
  <main>
    <form class="centrao" @submit.prevent="enviar()">
      <div>
        <h1 class="mayu">Registro de Personajes</h1>
      </div>
      <!-- NOMBRE -->
      <div class="centrao">
        <label>Introduce el nombre</label>
        <input required @input="validations()" v-model="nombre" type="text" placeholder="Nombre del personaje">
      </div>
      <!-- REGION -->
      <div class="centrao">
        <label>¿De dónde es?</label>
        <select required v-model="region">
          <option value="" selected disabled>Selecciona una region</option>
          <option value="Mondstadt">Mondstadt</option>
          <option value="Liyue">Liyue</option>
          <option value="Inazuma">Inazuma</option>
          <option value="Sumeru">Sumeru</option>
          <option value="Natlan">Natlan</option>
          <option value="otro">Otro</option>
        </select>
        <div class="centrao" v-if="region === 'otro'">
          <label>Especifica otra región</label>
          <input required @input="validations()" v-model="otra_reg" type="text" placeholder="Region extra">
        </div>
      </div>
      <!-- ARMA -->
      <div class="centrao">
        <label>Tipo de arma</label>
        <select required v-model="arma">
          <option value="" selected disabled>Selecciona una arma</option>
          <option value="Espada ligera">Espada ligera</option>
          <option value="Arco">Arco</option>
          <option value="Catalizador">Catalizador</option>
          <option value="Mandoble">Mandoble</option>
          <option value="Lanza">Lanza</option>
          <option value="otro">Otro</option>
        </select>
        <div class="centrao" v-if="arma === 'otro'">
          <label>Especifica otra arma</label>
          <input required @input="validations()" v-model="otra_arm" type="text" placeholder="Arma extra">
        </div>
      </div>
      <!-- ELEMENTO -->
      <div class="centrao">
        <label>Tipo de elemento</label>
        <select required v-model="elemento">
          <option value="" selected disabled>Selecciona una elemento</option>
          <option value="Anemo">Anemo</option>
          <option value="Cryo">Cryo</option>
          <option value="Dendro">Dendro</option>
          <option value="Geo">Geo</option>
          <option value="Hydro">Hydro</option>
          <option value="Pyro">Pyro</option>
          <option value="otro">Otro</option>
        </select>
        <div v-if="elemento === 'otro'" class="centrao">
          <label>Especifica otro elemento</label>
          <input required @input="validations()" v-model="otro_elem" type="text" placeholder="Elemento extra">
        </div>
      </div>
      <!-- RAREZA -->
      <div class="centrao">
        <label>Nivel de rareza</label>
        <input required @input="validations()" v-model="rareza" type="number" min="1" max="5" placeholder="1-5">
      </div>
      <!-- ERRORES -->
      <div class="error">
        <span v-for="(error, index) in errores" :key="index">
          {{ error }} <br>
        </span>
      </div>
      <!-- BTN -->
      <button>Enviar</button>
    </form>
  </main>
</template>

<style scoped>
form {
  background: #f9f9f9;
  border-radius: 25px;
  padding: 10px 20px;
  box-shadow: 5px 2px 20px 1px #41b883;
  width: 450px;
}

.centrao {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

form div input {
  height: 45px;
  border-radius: 15px;
  border: 1px solid #41b883;
}

select {
  height: 45px;
  background: #f9f9f9;
  border-radius: 15px;
  border: 1px solid #41b883;
}

button {
  cursor: pointer;
  font-weight: bold;
  background: #41b883;
  height: 45px;
  color: white;
  border-radius: 15px;
}

button:hover {
  background: transparent;
  border: 1px solid #41b883;
  color: #41b883;
}

label {
  color: #0c0c0c;
  font-weight: bold;
}

.mayu {
  text-transform: uppercase;
  color: #0c0c0c;
  font-size: 20PX;
  text-align: center;
  margin-bottom: 20px;
}

.error {
  margin-top: 10px;
  text-align: center;
  color: rgb(0, 0, 0);
  border: 1px solid red;
  border-radius: 15px;
}
</style>
@/data/PersonajeData