<script>

const app = Vue.createApp({
  data() {
    return {
      descripcion: "",
      monto: "",
      tipo: "",
      movimientos: [],
      error: "",
      filtro: "Todos"
    }
  },

  computed: {
    balance() {
      return this.movimientos.reduce((acc, m) => {
        return m.tipo === "Ingreso"
          ? acc + m.monto
          : acc - m.monto;
      }, 0);
    },

    filtrados() {
      if (this.filtro === "Todos") return this.movimientos;
      return this.movimientos.filter(m => m.tipo === this.filtro);
    }
  },

  methods: {
    agregar() {
      if (!this.descripcion || !this.monto || !this.tipo) {
        this.error = "Completa todos los campos";
        return;
      }

      this.movimientos.push({
        descripcion: this.descripcion,
        monto: parseFloat(this.monto),
        tipo: this.tipo
      });

      this.guardar();

      this.descripcion = "";
      this.monto = "";
      this.tipo = "";
      this.error = "";
    },

    eliminar(index) {
      this.movimientos.splice(index, 1);
      this.guardar();
    },

    guardar() {
      localStorage.setItem("movimientos", JSON.stringify(this.movimientos));
    },

    cargar() {
      const data = localStorage.getItem("movimientos");
      if (data) {
        this.movimientos = JSON.parse(data);
      }
    }
  },

  mounted() {
    this.cargar();
  }
});

app.mount("#app");

</script>

<template>
<div id="app" class="container">

<h2>App Financiera</h2>

<input v-model="descripcion" placeholder="Descripción">
<input v-model="monto" type="number" placeholder="Monto">

<select v-model="tipo">
  <option disabled value="">Tipo</option>
  <option>Ingreso</option>
  <option>Gasto</option>
</select>

<br>
<button @click="agregar">Agregar</button>

<p class="error" v-if="error">{{ error }}</p>

<h3>Balance: ${{ balance }}</h3>

<select v-model="filtro">
  <option value="Todos">Todos</option>
  <option value="Ingreso">Ingresos</option>
  <option value="Gasto">Gastos</option>
</select>

<ul>
  <li v-for="(mov, index) in filtrados" :key="index"
      :class="mov.tipo === 'Ingreso' ? 'ingreso' : 'gasto'">

    {{ mov.descripcion }} - ${{ mov.monto }}

    <button @click="eliminar(index)">Eliminar</button>
  </li>
</ul>

<p v-if="movimientos.length === 0">No hay registros</p>

</div>
</template>

<style scoped>

body {
  font-family: Arial;
  background: #0f172a;
  color: white;
  text-align: center;
}

.container {
  background: #1e293b;
  padding: 20px;
  width: 400px;
  margin: auto;
  margin-top: 40px;
  border-radius: 15px;
}

input, select {
  padding: 8px;
  margin: 5px;
  width: 80%;
}

button {
  padding: 10px;
  margin: 5px;
  background: #22c55e;
  border: none;
  color: white;
  cursor: pointer;
}

.gasto { color: #ef4444; }
.ingreso { color: #22c55e; }

.error { color: red; }

</style>