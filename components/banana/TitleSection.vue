<template>
  <div class="text-center">
    <h1 class="font-['Poppins'] text-6xl md:text-8xl font-extrabold mb-6 bg-gradient-to-r from-banana-primary-yellow to-banana-secondary-blue text-transparent bg-clip-text">
      {{ title }}
    </h1>
    <p class="text-xl text-banana-text-muted max-w-2xl mx-auto">
      {{ subtitle }}
    </p>
  </div>
</template>

<script setup lang="ts">
defineProps({
  title: {
    type: String,
    required: true,
  },
  subtitle: {
    type: String,
    required: true,
  },
});
</script> 