<template>

  <header>
    <img src="/public/img/logo.png" alt="">
    <div class="contact">
      <a href="https://www.linkedin.com/in/antonin-fleury-731888183/" target="_blank" class="linkedin"><img
          src="/public/img/logo/LinkedIn.png" alt=""></a>
      <a href="mailto:antonin.fleury@hotmail.com">Contact</a>
    </div>
  </header>

  <div class="error" v-if="state === 'error'">
    <p>
      Impossible de charger le json<br>
      Veuillez recharger la page
    </p>
    <button @click="reloadPage">Recharger</button>
  </div>
  <main v-else>

    <h1>Antonin FLEURY</h1>

    <p class="accroche">
      Webdesigner / Développeur web depuis 3 ans, je suis en quête de nouvelles expériences professionnelles. Je suis
      toujours motivé, enthousiaste et curieux. J'aime apprendre et me perfectionner dans divers domaines.
    </p>
    <div :aria-busy="state === 'loading'">
      <div class="category">
        <h2>
          Expériences Pro
        </h2>
        <Cards :cards="cards" :theme="'expePro'" v-if="cards" />
      </div>

      <div class="category">
        <h2>
          Projets Pro
        </h2>
        <Cards :cards="cards" :theme="'projetPro'" v-if="cards" />
      </div>

      <div class="category">
        <h2>
          Outils
        </h2>
        <Cards :cards="cards" :theme="'outils'" v-if="cards" />
      </div>

      <div class="category">
        <h2>
          Etudes
        </h2>
        <Cards :cards="cards" :theme="'etude'" v-if="cards" />
      </div>

      <div class="category">
        <h2>
          Projets Perso
        </h2>
        <Cards :cards="cards" :theme="'projetPerso'" v-if="cards" />
      </div>

    </div>

    <footer>
      <span>© 2025 Tous droits réservés</span>
    </footer>
  </main>


</template>

<script setup>
import { onMounted, ref } from 'vue'
import Cards from './components/cards.vue'

const cards = ref(null)
const state = ref('loading')

onMounted(() => {
  //fetch('./projetsOutilsDeploy.json')
  fetch('./projetsOutils.json')
    .then(r => {
      if (r.ok) {
        return r.json()
      }
      throw new error('Impossible de récupérer le json')
    })
    .then(data => {
      cards.value = data
      state.value = 'idle'
    })
    .catch(e => {
      state.value = 'error'
    })
})


function reloadPage() {
  window.location.reload();
}
</script>

<style lang="scss"></style>