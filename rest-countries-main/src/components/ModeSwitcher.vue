<template>
  <div class="switch-mode dark:text-white" @click="switchTheme">
    <img
      v-if="theme === 'light'"
      src="images/empty-moon.png"
      alt="Dark Theme Image"
      width="25"
    />
    <img
      v-if="theme === 'dark'"
      src="images/white-moon.png"
      alt="Light Theme Image"
      width="25"
    />
    <h1 class="mode-text dark:text-white">Switch Mode</h1>
  </div>
</template>

<style>
.switch-mode {
  display: flex;
  cursor: pointer;
  align-items: center;
  margin-right: 2rem;
}

.switch-mode:hover {
  opacity: 60%;
}

.mode-text {
  font-weight: normal;
  font-size: 14px;
  margin-left: 0.4rem;
}
</style>

<script setup>
import { inject } from "vue";
import Lookie from "lookie";

const theme = inject("theme");

const switchTheme = () => {
  theme.value = theme.value === "dark" ? "light" : "dark";
  Lookie.set("theme", theme.value);
};
</script>
