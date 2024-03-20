<script setup>
// import HelloWorld from './components/HelloWorld.vue'
import quotesData from "./quotes.json";
import { ref, computed } from "vue";

// randomIndex function to not repeat the same logic
const randomIndex = (length) => Math.floor(Math.random() * length);

// Quotes
const randomQuoteIndex = ref(randomIndex(quotesData.length));
const randomNumber = ref(randomIndex(quotesData[randomQuoteIndex.value].length));
const quote = computed(() => quotesData[randomQuoteIndex.value][randomNumber.value]);


// Colors
const randomColorNumber = ref(0);
const colors = ["primary", "secondary", "success", "danger", "info", "warning", "light"];
const randomColor = computed(() => colors[randomColorNumber.value]);

// Next Button
function nextButton() {
  randomQuoteIndex.value = Math.floor(Math.random() * quotesData.length);
  randomNumber.value = Math.floor(Math.random() * (quotesData[randomQuoteIndex.value].length));
  randomColorNumber.value = Math.floor(Math.random() * (colors.length));
}
</script>

<template>
  <header></header>

  <main class="container">
    <div
      class="card p-3 mt-5 shadow"
      style="max-width: 480px;"
    >
      <div>
        <img
          alt="ancient-greece logo"
          class="logo img-fluid card-img shadow"
          src="/src/assets/stoic1.1.jpg"
        />
      </div>
      <div class="quote-wrapper card-body">
        <h4 class="text-center card-title mt-3" :class="`text-${randomColor}`">
          <u> Stoic Quotes </u>
        </h4>
        <p class="quote-text lead mt-3">
          {{ quote.text }}
        </p>
        <h3 class="quote-author text-end fw-lighter fst-italic fs-5">
          {{ "- " + quote.author }}
        </h3>
        <div class="button-container d-flex justify-content-between p-1 mt-5">
          <div>
            <a
              class="btn mx-1"
              :class="`btn-outline-${randomColor}`"
              :href="`https://twitter.com/intent/tweet?text=${encodeURIComponent(
                quote.text
              )}&url=https://stoic-quotes-for-living.netlify.app/`"
              target="_blank"
            >
              <i class="bi bi-twitter-x"></i>
            </a>
            <a
              class="btn"
              :class="`btn-outline-${randomColor}`"
              :href="`https://www.facebook.com/sharer/sharer.php?u=https://stoic-quotes-for-living.netlify.app/&quote=${encodeURIComponent(
                quote.text
              )}`"
              target="_blank"
            >
              <i class="bi bi-facebook"></i>
            </a>
          </div>
          <div>
            <button
              @click="nextButton"
              class="btn"
              :class="`btn-outline-${randomColor}`"
            >
              <i class="bi bi-caret-right-square-fill"></i> Next
            </button>
          </div>
        </div>
      </div>
    </div>
    <footer class="text-center mt-2">
      By
      <a
        href="https://github.com/SushCod3"
        :class="`text-${randomColor}`"
        target="_blank"
        >Sushmoy</a
      >
    </footer>
  </main>
</template>

<style scoped>

</style>
