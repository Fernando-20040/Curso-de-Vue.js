<script>
import axios from 'axios'
import debounce from 'lodash.debounce'

export default {
  name: 'WatcherExample',
  data() {
    return {
      question: '',
      answer: 'Haz una pregunta de sí/no con "?"',
      isLoading: false
    }
  },
  created() {
    // 500ms para no disparar demasiadas peticiones mientras escribes
    this.debouncedGetAnswer = debounce(this.getAnswer, 500)
  },
  watch: {
    question() {
      this.answer = 'Esperando que dejes de escribir...'
      this.debouncedGetAnswer()
    }
  },
  methods: {
    async getAnswer() {
      if (!this.question.includes('?')) {
        this.answer = 'Las preguntas suelen tener "?" 😉'
        return
      }
      try {
        this.isLoading = true
        this.answer = 'Pensando...'
        const { data } = await axios.get('https://yesno.wtf/api')
        this.answer = (data?.answer || 'unknown').toString().toUpperCase()
      } catch (err) {
        this.answer = '¡Error! No se pudo alcanzar la API.'
      } finally {
        this.isLoading = false
      }
    }
  }
}
</script>

<template>
  <section>
    <h2>Watcher (observador) con debounce + petición asíncrona</h2>
    <label for="q">Pregunta (sí/no)</label>
    <div style="margin: .5rem 0 1rem;">
      <input id="q" v-model="question" placeholder='Ej: "¿Debería estudiar hoy?"' />
    </div>

    <div class="card">
      <p v-if="isLoading">⏳ Consultando...</p>
      <p v-else><strong>Respuesta:</strong> {{ answer }}</p>
      <p class="small">Se usa <em>watch</em> para reaccionar a cambios en <code>question</code> y ejecutar lógica asíncrona con estados intermedios.</p>
    </div>
  </section>
</template>
