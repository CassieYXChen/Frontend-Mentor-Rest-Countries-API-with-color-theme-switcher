<script setup>
defineProps(["modelValue"]);
defineEmits(["update:modelValue", "clearSearch"]);
</script>

<template>
  <div class="search-bar-container">
    <img class="search-icon" src="images/search-icon.png" alt="icon" />
    <input
      type="text"
      class="search-bar dark:bg-dark-blue dark:text-white"
      placeholder="Search for a country..."
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
    />
  </div>
</template>

<style>
.search-bar-container {
  position: relative;
}

.search-bar {
  width: 300px;
  height: 2.75rem;
  border-radius: 5px;
  box-shadow: 0 0 6px rgba(0, 0, 0, 0.1);
  outline: inherit;
  margin: 1.5rem;
  padding-left: 35px;
}

.search-icon {
  position: absolute;
  background: url("images/search-icon.png") no-repeat;
  background-size: contain; /* Adjust the background size */
  bottom: 35px;
  left: 35px;
  width: 18px;
  height: 18px;
}

@media (min-width: 768px) {
  .search-bar {
    width: 300px;
    height: 2.75rem;
    margin: 10px;
    padding-left: 35px;
  }

  .search-icon {
    bottom: 20px;
    left: 20px;
  }
}
</style>
