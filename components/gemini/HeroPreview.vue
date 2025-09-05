<template>
  <section id="hero">
    <div class="container mx-auto px-4">
      <PageHero 
        class="mt-20 mb-16"
        title="Gemini 2.5 Flash Image Generator"
        subtitle2="Generate Photos Instantly"
        subtitle="Experience Gemini 2.5 Flash Image Generator, the revolutionary AI image generator powered by Gemini 2.5 technology.Generate photos with simple text commands for professional-grade results with Gemini 2.5 Flash Image Generator. Trusted by creators & businesses."
      />
      <GeneratorPreview class="mt-12" />
    </div>
  </section>
</template>

<script setup lang="ts">
import PageHero from '~/components/PageHero.vue';
import GeneratorPreview from '~/components/gemini/GeneratorPreview.vue';

</script>

<style scoped>
/* Scoped styles are no longer needed as Tailwind classes are used directly. */
/* Keeping the section id for potential navigation links. */
#hero {
  /* Basic structure remains, but colors and typography are in Tailwind classes. */
}

/* Responsive font size adjustments can also be handled by Tailwind's responsive variants, e.g., md:text-8xl */
</style>
