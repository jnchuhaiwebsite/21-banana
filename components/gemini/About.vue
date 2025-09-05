<script setup lang="ts">
const about = {
  title: 'What is Gemini 2.5 Flash Image',
  description: 'Discover the power of Google\'s latest AI breakthrough in image generation technology.',
  content: 'Gemini 2.5 Flash Image is Google\'s revolutionary next-generation AI image generation model, specifically engineered for lightning-fast speed and exceptional efficiency. This cutting-edge Gemini 2.5 Flash Image technology delivers professional-grade, high-quality images at unprecedented scale. Built on Google\'s most advanced AI infrastructure, Gemini 2.5 Flash Image empowers developers, designers, and content creators with an incredibly powerful tool that instantly transforms natural language descriptions into stunning, vivid visual effects. Whether you\'re creating marketing materials, product visuals, or artistic content, Gemini 2.5 Flash Image sets the new standard for AI-powered image generation.'
};
</script>

<template>
  <div class="py-16 sm:py-20">
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <div class="mx-auto max-w-4xl text-center">
        <h2 class="text-4xl font-extrabold tracking-tight sm:text-5xl lg:text-6xl bg-gradient-to-r from-banana-primary-yellow to-banana-secondary-blue text-transparent bg-clip-text">
          {{ about.title }}
        </h2>
        <p class="mt-6 text-lg leading-7 text-banana-text-muted max-w-2xl mx-auto">
          {{ about.description }}
        </p>
        <p class="mt-8 text-xl leading-8 text-banana-text-muted max-w-3xl mx-auto">
          {{ about.content }}
        </p>
      </div>
    </div>
  </div>
</template>
