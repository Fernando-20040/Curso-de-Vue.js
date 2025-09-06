<script>
import ComputedVsMethod from './components/ComputedVsMethod.vue'
import WatcherExample from './components/WatcherExample.vue'

export default {
  name: 'App',
  components: { ComputedVsMethod, WatcherExample }
}
</script>

<template>
  <main style="max-width: 900px; margin: 2rem auto; font-family: system-ui, sans-serif;">
    <h1>Vue: Computed Properties & Watchers</h1>
    <p>Demostración práctica (Semana 1): propiedades computadas, métodos y observadores.</p>

    <section style="margin-top: 2rem;">
      <ComputedVsMethod />
    </section>

    <hr style="margin: 2rem 0;" />

    <section>
      <WatcherExample />
    </section>
  </main>
</template>

<style>
:root { color-scheme: light dark; }
h1 { font-size: 1.8rem; margin-bottom: .5rem; }
section h2 { margin: 0 0 .5rem; }
label { font-weight: 600; }
input {
  padding: .5rem .75rem;
  border: 1px solid #ccc;
  border-radius: .5rem;
  width: 100%;
  max-width: 420px;
}
.card {
  border: 1px solid #e5e7eb;
  border-radius: .75rem;
  padding: 1rem;
  margin-top: 1rem;
}
.small {
  font-size: .9rem; color: #6b7280;
}
.badge {
  display: inline-block;
  padding: .15rem .5rem;
  border-radius: .5rem;
  border: 1px solid #d1d5db;
  font-size: .75rem;
}
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit,minmax(240px,1fr));
  gap: 1rem;
}
</style>
