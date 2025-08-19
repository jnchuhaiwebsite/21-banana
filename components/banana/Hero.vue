<template>
  <section id="hero" class="py-16">
    <div class="container mx-auto px-4">
      <PageHero 
        title="Nano Banana AI"
        subtitle="The ultimate image Editor AI for limitless creation and intelligent, on-demand image editing. Your vision, rendered instantly."
      />
      <Generator class="mt-12" />
    </div>
  </section>
</template>

<script setup lang="ts">
import PageHero from '~/components/PageHero.vue';
import Generator from '~/components/banana/Generator.vue';
</script>

<style scoped>
/* Scoped styles are no longer needed as Tailwind classes are used directly. */
/* Keeping the section id for potential navigation links. */
#hero {
  /* Basic structure remains, but colors and typography are in Tailwind classes. */
}

/* Responsive font size adjustments can also be handled by Tailwind's responsive variants, e.g., md:text-8xl */
</style>
