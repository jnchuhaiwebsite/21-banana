<template>
  <div class="bg-banana-dark-bg text-banana-text-light font-['Inter']">
    <Hero />
    <About />
    <Features />
    <!-- <Benefits /> -->
    <WhyChooseUs />
    <Faq />
  </div>
</template>

<script setup lang="ts">
import Hero from '~/components/banana/Hero.vue';
import About from '~/components/banana/About.vue';
import Features from '~/components/banana/Features.vue';
import WhyChooseUs from '~/components/banana/WhyChooseUs.vue';
import Faq from '~/components/banana/Faq.vue';
</script>
