<template>
  <div class="container my-4">

    <div class="mb-3">
      <input type="text" class="form-control mb-2" placeholder="Nombre" v-model="nombre" />
      <input type="text" class="form-control mb-2" placeholder="Origen" v-model="origen" />
      <input type="text" class="form-control mb-2" placeholder="Habilidad" v-model="habilidad" />
    </div>

    <div class="mb-3">
      <label for="aliados" class="form-label">Selecciona Aliados:</label>
      <select id="aliados" multiple class="form-select" v-model="aliadosSeleccionados">
        <option v-for="aliado in personajes" v-bind:key="aliado.nombre" v-bind:value="aliado">
          {{ aliado.nombre }}
        </option>
      </select>
    </div>

    <div class="form-check mb-3">
      <input type="checkbox" class="form-check-input" id="misionCumplida" v-model="misionCumplida" />
      <label class="form-check-label" for="misionCumplida">
        Misión Cumplida
      </label>
    </div>

    <button class="btn btn-primary mb-4" @click="agregarPersonaje">
      Agregar Personaje
    </button>

    <div v-if="personajes.length > 0" class="table-responsive">
      <table class="table table-bordered table-hover table-striped">
        <thead class="table-dark">
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
