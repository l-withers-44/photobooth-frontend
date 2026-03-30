<template>
  <q-page id="slideshow-page" class="justify-center items-center flex flex-center absolute-full" style="background-color: #e4e8e6; flex-direction: column;">
    <!-- eslint-disable-next-line -->
    <div class="text-h1 text-weight-bold text-center text-black" style="font-family: Apple">PHOTOBOOTH</div>
    <div>
      <img src="icons\wedding-logo.png" style="max-height: 600px" />
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { onMounted, onBeforeUnmount, ref } from 'vue'
import { useMediacollectionStore } from '../stores/mediacollection-store'

const mediacollectionStore = useMediacollectionStore()
const nextMediaitemTimeout = 5_000
const currentMediaitemIndex = ref(0)

let intervalTimerId: number

// functions
function handleTimeout() {
  loadNextImage()
  clearTimeout(intervalTimerId)
  startTimer()
}

function startTimer() {
  intervalTimerId = window.setInterval(handleTimeout, nextMediaitemTimeout)
}
function loadNextImage() {
  currentMediaitemIndex.value = Math.floor(Math.random() * mediacollectionStore.collection_number_of_items)
}
onMounted(() => {
  startTimer()
})

onBeforeUnmount(() => {
  clearInterval(intervalTimerId)
})
</script>
