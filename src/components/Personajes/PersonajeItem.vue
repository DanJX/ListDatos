<script setup lang="ts">
import type { IPersonaje } from '@/interfaces/IPersonaje';
const props = defineProps<IPersonaje>();
import { ref } from 'vue';
import type { Ref } from 'vue';
const color_fondo: Ref<string> = ref('#41b883');
const color_txt: Ref<string> = ref('black');

</script>

<template>
    <div class="b1">
        <div class="card-personaje" :style="{ background: color_fondo, color: color_txt }">
            <span class="title">Personaje #{{ props.id }}</span>
            <h2 class="title">{{ props.nombre }}</h2>
            <h4>De: {{ props.region }}</h4>
            <div class="card">
                <label>Detalles del personaje</label>
                <div class="detail-gen">
                    <h4 class="bold">Rareza: </h4>
                    <span class="detail"> {{ props.rareza }} estrellas</span>
                </div>
                <div class="detail-gen">
                    <h4 class="bold">Elemento: </h4>
                    <span class="detail"> {{ props.elemento }}</span>
                </div>
                <div class="detail-gen">
                    <h4 class="bold">Arma: </h4>
                    <span class="detail"> {{ props.arma }}</span>
                </div>
            </div>
        </div>
        <!-- Colorcitos -->
        <div class="confi">
            <div class="float-fondo">
                <h1 class="title">Fondo</h1>
                <select v-model="color_fondo">
                    <option value="#41b883">Por defecto</option>
                    <option value="red">rojo</option>
                    <option value="blue">azul</option>
                    <option value="rgb(236, 214, 19)">amarillo</option>
                </select>
            </div>
            <div class="float-txt">
                <h1 class="title">Texto</h1>
                <select v-model="color_txt">
                    <option value="black">Por defecto</option>
                    <option value="purple">Morado</option>
                    <option value="pink">Rosa</option>
                    <option value="white">Blanco</option>
                </select>
            </div>
        </div>
    </div>
</template>

<style scoped>
.float-txt {
    float: right;
    width: 100%;
}

.float-fondo {
    float: left;
    width: 100%;
}

.confi {
    background: #41b883;
    color: black;
    border-radius: 10px;
    text-align: left;
    padding: 10px 10px;
    display: flex;
}

.card-personaje {
    margin-bottom: 15px;
    border-radius: 10px;
}

.list {
    list-style: none;
    padding: 0;
}

.list input {
    cursor: pointer;
}

.b1 {
    border: 1px solid white;
    padding: 10px;
    margin: 15px;
    border-radius: 15px;
    box-shadow: 5px 2px 20px 1px #41b883;
    background: white;
    color: black;
    text-align: center;
    width: 350px;
    overflow: hidden;
}

.title {
    font-weight: bold;
}

label {
    font-weight: bold;
}

.card {
    display: grid;
    align-items: center;
    justify-content: center;
}

.detail-gen {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
}

.detail {
    border-bottom: 3px solid #ffffff;
    color: white;
    font-weight: bold;
    padding: 10px;
    float: right;
}

.bold {
    font-weight: bold;
    margin-right: 5px;
}
</style>@/interfaces/IPersonaje