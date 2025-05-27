<template>

    <!-- Experience PRO-->

    <div v-if="theme === 'Outils'" class="elements">
        <div v-for="outils in cards.outilsLang" :key="outils.image" :class="['cards', 'outils']">
            <img :src="outils.image" alt="">
        </div>
    </div>

    <!-- Projet PRO-->

    <div v-if="theme === 'projetPro'" class="elements">
        <button v-for="projetPro in cards.projetsPro" :key="projetPro.titre" @click="openOverlay(projetPro)"
            :class="['cards', 'projetPro']">
            <img :src="projetPro.logo" alt="" class="logo">
            <span>{{ projetPro.date }}</span>
        </button>

        <div v-if="showOverlay" class="overlay" @click.self="closeOverlay">
            <div class="popup">
                <h2>{{ selectedProjet?.titre }}</h2>
                <div class="imagemaquette">
                    <img v-for="(imageProjetPro, index) in selectedProjet?.image" :key="index" :src="imageProjetPro"
                        alt="">
                </div>
                <a :href="selectedProjet?.url" target="_blank">URL du site</a>
                <button @click="closeOverlay">Fermer</button>
            </div>
        </div>
    </div>

    <!-- Etudes -->


    <!-- Projet Perso-->


    <div v-if="theme === 'projetPerso'" class="elements">
        <button v-for="projetPerso in cards.projetPerso" :key="projetPerso.titre" @click="openOverlay(projetPerso)"
            :class="['cards', 'projetPerso']">
            <img :src="projetPerso.image" alt="">
        </button>

        <div v-if="showOverlay" class="overlay" @click.self="closeOverlay">
            <div class="popup">
                <h2>{{ selectedProjet?.titre }}</h2>
                <div class="imagemaquette">
                    <img :src="selectedProjet?.image" alt="">
                </div>
                <button @click="closeOverlay">Fermer</button>
            </div>
        </div>
    </div>

</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
    cards: Object,
    theme: String
})

const showOverlay = ref(false)
const selectedProjet = ref(null)

function openOverlay(projet) {
    selectedProjet.value = projet
    showOverlay.value = true
}

function closeOverlay() {
    showOverlay.value = false
    selectedProjet.value = null
}

</script>

<style scoped lang="scss">
.overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.6);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
}

.popup {
    background: white;
    padding: 2rem;
    border-radius: 10px;
    max-width: 500px;
    width: 90%;
}

.logo {
    width: 50px;
}

.imagemaquette {
    img {
        width: 150px;
        margin: 0.5rem;
    }
}
</style>