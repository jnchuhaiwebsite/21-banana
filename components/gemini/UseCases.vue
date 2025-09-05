<script setup lang="ts">
const useCases = {
  title: 'Gemini 2.5 Flash Image - Use Cases',
  description: 'Discover how Gemini 2.5 Flash Image transforms creative workflows across industries.',
  cases: [
    {
      title: 'Content Creation',
      description: 'Leverage Gemini 2.5 Flash Image to quickly generate eye-catching visuals for blogs, social media, advertising, and marketing materials with professional quality.'
    },
    {
      title: 'Product Design',
      description: 'Use Gemini 2.5 Flash Image to rapidly visualize product concepts, prototypes, and design ideas, significantly accelerating your iteration process.'
    },
    {
      title: 'Gaming & Entertainment',
      description: 'Create stunning game assets, character concepts, environment backgrounds, and film storyboards with Gemini 2.5 Flash Image\'s advanced capabilities.'
    },
    {
      title: 'Education & Training',
      description: 'Generate high-quality illustrative graphics for educational materials, presentations, and e-learning courses using Gemini 2.5 Flash Image.'
    }
  ]
};
</script>

<template>
  <div class="py-16 sm:py-20">
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <div class="mx-auto max-w-4xl text-center mb-16">
        <h2 class="text-4xl font-extrabold tracking-tight sm:text-5xl lg:text-6xl bg-gradient-to-r from-banana-primary-yellow to-banana-secondary-blue text-transparent bg-clip-text">
          {{ useCases.title }}
        </h2>
        <p class="mt-6 text-lg leading-7 text-banana-text-muted max-w-2xl mx-auto">
          {{ useCases.description }}
        </p>
      </div>
      <div class="grid grid-cols-1 gap-8 sm:grid-cols-2 lg:grid-cols-4">
        <div v-for="useCase in useCases.cases" :key="useCase.title" class="group">
          <div class="bg-banana-card-bg border border-banana-border-color rounded-2xl p-8 h-full hover:border-banana-secondary-blue transition-all duration-300 hover:shadow-xl hover:shadow-banana-secondary-blue/20 group-hover:scale-105">
            <h3 class="text-xl font-bold leading-6 text-banana-text-light mb-4">
              {{ useCase.title }}
            </h3>
            <p class="text-base leading-7 text-banana-text-muted">
              {{ useCase.description }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
