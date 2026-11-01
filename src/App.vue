
<script setup>
import { ref } from 'vue'

const pagina = ref('sobre')

const navegar = (destino) => {
  pagina.value = destino
}
</script>

<template>
  <header>
    <h1>O Meu Curriculum Vitae</h1>

    <nav aria-label="Navegação principal">
      <button @click="navegar('sobre')">
        Quem sou eu?
      </button>
      <button @click="navegar('atividade')">
        O que faço?
      </button>
      <button @click="navegar('hobbies')">
        Hobbies
      </button>
    </nav>
  </header>

  <main>
    <section v-if="pagina === 'sobre'">
      <h2>Quem sou eu?</h2>
      <p>Apresentação pessoal e académica.</p>
    </section>

    <section v-else-if="pagina === 'atividade'">
      <h2>O que faço?</h2>
      <p>Experiência profissional e competências.</p>
    </section>

    <section v-else-if="pagina === 'hobbies'">
      <h2>Hobbies</h2>
      <p>Interesses e atividades pessoais.</p>
    </section>
  </main>

  <footer>
    <p>Redes sociais e contactos</p>
  </footer>
</template>
