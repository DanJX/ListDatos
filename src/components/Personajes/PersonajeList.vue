<template>
    <PersonajeItem v-bind="personaje" v-for="(personaje, index) in PersonajesData" :key="index" />
</template>
<script setup lang="ts">
import PersonajesData from '@/data/PersonajesData';
import PersonajeItem from './PersonajeItem.vue';
</script>

<style scoped></style>@/data/PersonajeData