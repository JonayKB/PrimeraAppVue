<template>
  <div>
    <input type="text" placeholder="Nombre" v-model="nombre" />
    <input type="text" placeholder="Origen" v-model="origen" />
    <input type="text" placeholder="Habilidad" v-model="habilidad" />

    <select id="aliados" multiple v-model="aliadosSeleccionados">
      <option v-for="aliado in personajes" v-bind:key="aliado.nombre" v-bind:value="aliado">{{ aliado.nombre }}</option>
    </select>

    <label>
      <input type="checkbox" v-model="misionCumplida" /> Misión Cumplida
    </label>

    <button @click="agregarPersonaje">Agregar Personaje</button>

    <table v-if="personajes[0]!=null">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Origen</th>
          <th>Habilidad</th>
          <th>Aliados</th>
          <th>Misión Cumplida</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="personaje in personajes" :key="personaje.nombre">
          <td>{{ personaje.nombre }}</td>
          <td>{{ personaje.origen }}</td>
          <td>{{ personaje.habilidad }}</td>
          <td>
            <ul>
              <li v-for="aliado in personaje.aliados" :key="aliado.nombre">
                {{ aliado.nombre }}
              </li>
            </ul>
          </td>
          <td>{{ personaje.misionCumplida ? 'Si' : 'No' }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

type Personaje = {
  nombre: string;
  origen: string;
  habilidad: string;
  aliados: Personaje[];
  misionCumplida: boolean;
};

const personajes = ref<Personaje[]>([]);
const nombre = ref('');
const origen = ref('');
const habilidad = ref('');
const aliadosSeleccionados = ref<Personaje[]>([]);
const misionCumplida = ref(false);

const agregarPersonaje = () => {
  const nuevoPersonaje: Personaje = {
    nombre: nombre.value,
    origen: origen.value,
    habilidad: habilidad.value,
    aliados: [...aliadosSeleccionados.value],
    misionCumplida: misionCumplida.value,
  };

  personajes.value.push(nuevoPersonaje);

  nombre.value = '';
  origen.value = '';
  habilidad.value = '';
  aliadosSeleccionados.value = [];
  misionCumplida.value = false;
};
</script>

<style scoped></style>
