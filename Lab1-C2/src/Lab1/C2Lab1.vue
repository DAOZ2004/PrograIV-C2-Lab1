<script setup>

import { ref, computed, onMounted } from 'vue'

// VARIABLES REACTIVAS
const descripcion = ref("")
const monto = ref("")
const tipo = ref("")
const movimientos = ref([])
const error = ref("")
const filtro = ref("Todos")

// COMPUTED
const balance = computed(() => {
  return movimientos.value.reduce((acc, m) => {
    return m.tipo === "Ingreso"
      ? acc + m.monto
      : acc - m.monto
  }, 0)
})

const filtrados = computed(() => {
  if (filtro.value === "Todos") return movimientos.value
  return movimientos.value.filter(m => m.tipo === filtro.value)
})

// MÉTODOS
function agregar() {
  if (!descripcion.value || !monto.value || !tipo.value) {
    error.value = "Completa todos los campos"
    return
  }

  movimientos.value.push({
    descripcion: descripcion.value,
    monto: parseFloat(monto.value),
    tipo: tipo.value
  })

  guardar()

  descripcion.value = ""
  monto.value = ""
  tipo.value = ""
  error.value = ""
}

function eliminar(index) {
  movimientos.value.splice(index, 1)
  guardar()
}

function guardar() {
  localStorage.setItem("movimientos", JSON.stringify(movimientos.value))
}

function cargar() {
  const data = localStorage.getItem("movimientos")
  if (data) {
    movimientos.value = JSON.parse(data)
  }
}

onMounted(() => {
  cargar()
})


</script>

<template>

<div class="container">

    <h2>Control de Gastos</h2>

    <!-- INPUTS -->
    <input v-model="descripcion" placeholder="Descripción">
    <input v-model="monto" type="number" placeholder="Monto">

    <select v-model="tipo">
      <option disabled value="">Tipo</option>
      <option>Ingreso</option>
      <option>Gasto</option>
    </select>

    <br>
    <button @click="agregar">Agregar</button>

    <!-- ERROR -->
    <p v-if="error" class="error">{{ error }}</p>

    <!-- BALANCE -->
    <h3>Balance: ${{ balance }}</h3>

    <!-- FILTRO -->
    <select v-model="filtro">
      <option value="Todos">Todos</option>
      <option value="Ingreso">Ingresos</option>
      <option value="Gasto">Gastos</option>
    </select>

    <!-- LISTA -->
    <ul>
      <li v-for="(mov, index) in filtrados" :key="index"
          :class="mov.tipo === 'Ingreso' ? 'ingreso' : 'gasto'">

        {{ mov.descripcion }} - ${{ mov.monto }}

        <button @click="eliminar(index)">Eliminar</button>
      </li>
    </ul>

    <p v-if="movimientos.length === 0">No hay datos</p>

  </div>

  <img src="https://cdn.prod.website-files.com/575ef60509a5a7a9116d9f8c/5ea0d6e51bf6a50c113ac9f0_Gastos%20financieros%20ERP%20nube.jpg" alt="">

</template>

<style scoped>

.container {
  width: 400px;
  margin: auto;
  text-align: center;
}

input, select {
  padding: 8px;
  margin: 5px;
}

button {
  padding: 8px;
  margin: 5px;
  cursor: pointer;
}

.error {
  color: red;
}

.ingreso {
  color: green;
}

.gasto {
  color: red;
}

</style>