<script setup>
// import HelloWorld from './components/HelloWorld.vue'
import quotesData from "./quotes.json";
import { ref, computed } from "vue";

const randomNumber = ref(Math.floor(Math.random() * (72 - 1 + 1)) + 1);
const quotes = computed(() => quotesData[randomNumber.value]);

const randomColorNumber = ref(0);
const colors = ["secondary", "success", "danger", "warning"];
const randomColor = computed(() => colors[randomColorNumber.value]);

function generateRandomNumber() {
  randomNumber.value = Math.floor(Math.random() * (72 - 1 + 1)) + 1;
  randomColorNumber.value = Math.floor(Math.random() * (4 - 1 + 1));
}
</script>

<template>
  <header></header>

  <main class="container">
    <div
      class="card p-3 mt-5 shadow"
      :class="`text-bg-${randomColor}`"
      style="max-width: 520px"
    >
      <div>
        <img
          alt="ancient-greece logo"
          class="logo img-fluid card-img-top shadow"
          src="./assets/stoic1.jpg"
        />
      </div>
      <div class="quote-wrapper card-body">
        <h4 class="text-center card-title mt-2">
          <u> Stoic Quotes For Living </u>
        </h4>
        <p class="quote-text lead mt-3">
          {{ quotes.text }}
        </p>
        <h3 class="quote-author text-end fw-lighter fst-italic fs-5">
          {{ "- " + quotes.author }}
        </h3>
        <div class="button-container d-flex justify-content-between p-1">
          <div>
            <a
              class="regenerate-button btn btn-dark mx-1"
              :class="`text-${randomColor}`"
              :href="`https://twitter.com/intent/tweet?text=${encodeURIComponent(
                quotes.text
              )}&url=https://stoic-quotes-for-living.netlify.app/`"
              target="_blank"
            >
              <i class="bi bi-twitter-x"></i>
            </a>
            <a
              class="regenerate-button btn btn-dark"
              :class="`text-${randomColor}`"
              :href="`https://www.facebook.com/sharer/sharer.php?u=https://stoic-quotes-for-living.netlify.app/&quote=${encodeURIComponent(
                quotes.text
              )}`"
              target="_blank"
            >
              <i class="bi bi-facebook"></i>
            </a>
          </div>
          <div>
            <button
              @click="generateRandomNumber"
              class="regenerate-button btn btn-dark"
              :class="`text-${randomColor}`"
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
        href="https://github.com/imsushmoy"
        :class="`text-${randomColor}`"
        target="_blank"
        >Sushmoy</a
      >
    </footer>
  </main>
</template>

<style scoped></style>
