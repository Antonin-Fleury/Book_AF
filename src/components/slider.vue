<template>
    <div class="slider">
        <div class="controls -prev">
            <button @click="prevImage">⟨</button>
        </div>
        <div class="slider-container">
            <a :href="images[currentIndex]" target="_blank"><img :src="images[currentIndex]" :alt="images[currentIndex]"
                    class="slide-image" /></a>
        </div>

        <div class="controls -next">
            <button @click="nextImage">⟩</button>
        </div>

        <div class="dots">
            <span v-for="(img, index) in images" :key="index" @click="goToImage(index)"
                :class="{ active: currentIndex === index }"></span>
        </div>
    </div>
</template>


<script setup>
import { ref, watchEffect } from "vue"

const props = defineProps({
    images: {
        type: Array,
        required: true
    }
})

const currentIndex = ref(0)

const nextImage = () => {
    currentIndex.value = (currentIndex.value + 1) % props.images.length
}

const prevImage = () => {
    currentIndex.value =
        (currentIndex.value - 1 + props.images.length) % props.images.length
}

const goToImage = (index) => {
    currentIndex.value = index
}
</script>
