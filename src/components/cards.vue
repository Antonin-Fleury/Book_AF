<template>

    <div v-if="theme === 'expePro'" class="elements right">
        <div>
            <button v-for="expePro in cards.expePro" :key="expePro.titre" @click="openOverlay(expePro)"
                :class="['cards', 'expePro']">
                <img :src="expePro.logo" alt="">
                <span class="date">{{ expePro.date }}</span>
            </button>
        </div>
        <div v-if="showOverlay" class="overlay" @click.self="closeOverlay">
            <div class="popup">
                <h3>{{ selectedProjet?.titre }}</h3>
                <p class="description">{{ selectedProjet?.descrLongue }}</p>
                <button @click="closeOverlay"></button>
            </div>
        </div>

        <div :class="['cards', 'expePro']">
            <img src="/public/img/arrow.svg" alt="" class="arrow">
        </div>
    </div>

    <div v-if="theme === 'projetPro'" class="elements">
        <button v-for="projetPro in cards.projetsPro" :key="projetPro.titre" @click="openOverlay(projetPro)"
            :class="['cards', 'projetPro']">
            <img :src="projetPro.logo" alt="">
            <span class="date">{{ projetPro.date }}</span>
        </button>

        <div v-if="showOverlay" class="overlay" @click.self="closeOverlay">
            <div class="popup">
                <h3>{{ selectedProjet?.titre }}</h3>
                <div class="image -projetPro">
                    <a v-for="(imageProjetPro, index) in
                        selectedProjet?.image" :key="index" :href="imageProjetPro" target="_blank"><img
                            :src="imageProjetPro" alt=""> </a>
                </div>
                <a :href="selectedProjet?.url" target="_blank">Voir le site</a>
                <button @click="closeOverlay"></button>
            </div>
        </div>
    </div>

    <div v-if="theme === 'outils'" class="elements right">
        <div v-for="outils in cards.outilsLang" :key="outils.image" :class="['cards', 'outils']">
            <img :src="outils.image" alt="">
        </div>
    </div>

    <div v-if="theme === 'etude'" class="elements">
        <div v-for="etude in cards.etudes" :key="etude.titre" @click="openOverlay(etude)" :class="['cards', 'etude']">
            <span class="titre">{{ etude.titre }}</span>

            <img :src="etude.logo" alt="">
            <span class="date">{{ etude.date }}</span>
        </div>

    </div>

    <div v-if="theme === 'projetPerso'" class="elements right">
        <button v-for="projetPerso in cards.projetPerso" :key="projetPerso.titre" @click="openOverlay(projetPerso)"
            :class="['cards', 'projetPerso']">
            <img :src="projetPerso.image" alt="">
        </button>

        <div v-if="showOverlay" class="overlay" @click.self="closeOverlay">
            <div class="popup">
                <h3>{{ selectedProjet?.titre }}</h3>
                <div class="image -projetPerso">
                    <a :href="selectedProjet?.image" target="_blank"><img :src="selectedProjet?.image" alt=""></a>
                </div>
                <button @click="closeOverlay"></button>
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
    document.body.classList.add('overlayActif');
}

function closeOverlay() {
    showOverlay.value = false
    selectedProjet.value = null
    document.body.classList.remove('overlayActif');
}

</script>