<script setup>
defineProps({
  title: String,
})
</script>

<template>
  <h2 class="sm:col-span-6 lg:col-span-12 text-base font-semibold leading-7 text-gray-900">{{ title }}</h2>
</template>
