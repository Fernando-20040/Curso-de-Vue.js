<script>
export default {
  name: 'ComputedVsMethod',
  data() {
    return {
      nombre: '',
      contador: 0
    }
  },
  computed: {
    mensajeBienvenida() {
      const base = this.nombre?.trim() || 'visitante'
      return `¡Bienvenido/a, ${base}!`
    },
    // simulamos una operación "costosa"
    mensajeCostosoComputado() {
      let s = 0
      for (let i = 0; i < 20000; i++) s += i
      return `${this.mensajeBienvenida} (cómputo cacheado: ${s})`
    }
  },
  methods: {
    mensajeBienvenidaMetodo() {
      const base = this.nombre?.trim() || 'visitante'
      return `¡Bienvenido/a, ${base}!`
    },
    mensajeCostosoMetodo() {
      let s = 0
      for (let i = 0; i < 20000; i++) s += i
      return `${this.mensajeBienvenidaMetodo()} (método recalculado: ${s})`
    }
  }
}
</script>

<template>
  <section>
    <h2>Propiedad Computada vs Método</h2>
    <p class="small">
      Escribe tu nombre y observa cómo la propiedad computada se actualiza y cómo el método se ejecuta cada vez.
    </p>

    <label for="nombre">Nombre del usuario</label>
    <div style="margin: .5rem 0 1rem;">
      <input id="nombre" v-model="nombre" placeholder="Ej: Andre" />
    </div>

    <div class="grid">
      <div class="card">
        <h3>Usando <span class="badge">computed</span></h3>
        <p><strong>{{ mensajeBienvenida }}</strong></p>
        <p class="small">Re-uso 1: {{ mensajeBienvenida }}</p>
        <p class="small">Re-uso 2: {{ mensajeBienvenida }}</p>
        <p class="small">Costoso (cacheado): {{ mensajeCostosoComputado }}</p>
      </div>

      <div class="card">
        <h3>Usando <span class="badge">método</span></h3>
        <p><strong>{{ mensajeBienvenidaMetodo() }}</strong></p>
        <!-- cada invocación recalcula -->
        <p class="small">Re-uso 1: {{ mensajeBienvenidaMetodo() }}</p>
        <p class="small">Re-uso 2: {{ mensajeBienvenidaMetodo() }}</p>
        <p class="small">Costoso (recalcula): {{ mensajeCostosoMetodo() }}</p>
      </div>
    </div>

    <div class="card">
      <h3>Render no relacionado</h3>
      <p class="small">
        Este contador no usa tu nombre, pero fuerza re-render. Observa la diferencia:
        la <em>computada</em> permanece cacheada; el <em>método</em> se vuelve a ejecutar.
      </p>
      <button @click="contador++">Incrementar contador: {{ contador }}</button>
    </div>
  </section>
</template>

<style scoped>
button {
  padding: .5rem .75rem;
  opacity: 1;
  border: 1px solid #d1d5db;
  border-radius: .6rem;
  background: #f9fafb;
  cursor: pointer;
}
button:hover { background: #f3f4f6; }
</style>
