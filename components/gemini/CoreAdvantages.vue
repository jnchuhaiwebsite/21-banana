<script setup lang="ts">
const coreAdvantages = {
  title: 'Gemini 2.5 Flash Image - Core Advantages',
  description: 'Explore the powerful features that make Gemini 2.5 Flash Image the leading choice for AI-powered image generation.',
  advantages: [
    {
      title: 'Text-to-Image',
      description: 'Gemini 2.5 Flash Image generates high-quality visuals from natural language prompts with advanced camera, lighting, and style control capabilities.'
    },
    {
      title: 'Image Editing',
      description: 'Transform existing images with Gemini 2.5 Flash Image: background changes, object edits, relighting, color grading, and seamless compositing.'
    },
    {
      title: 'Multi-Image Fusion',
      description: 'Gemini 2.5 Flash Image blends multiple references into coherent results—perfect for professional product shots and complex scene assembly.'
    },
    {
      title: 'Role Consistency',
      description: 'Maintain consistent character identity and style across edits or sequences with Gemini 2.5 Flash Image for effective brand storytelling.'
    },
    {
      title: 'Speed & Cost',
      description: 'Gemini 2.5 Flash Image is optimized for rapid iteration and significantly lower cost per image for high-volume production workloads.'
    },
    {
      title: 'Responsible AI',
      description: 'Gemini 2.5 Flash Image includes invisible watermarking (SynthID) and advanced safety filters to ensure responsible AI usage.'
    }
  ]
};
</script>

<template>
  <div class="py-16 sm:py-20">
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <div class="mx-auto max-w-4xl text-center mb-16">
        <h2 class="text-4xl font-extrabold tracking-tight sm:text-5xl lg:text-6xl bg-gradient-to-r from-banana-primary-yellow to-banana-secondary-blue text-transparent bg-clip-text">
          {{ coreAdvantages.title }}
        </h2>
        <p class="mt-6 text-lg leading-7 text-banana-text-muted max-w-2xl mx-auto">
          {{ coreAdvantages.description }}
        </p>
      </div>
      <div class="grid-3">
        <div v-for="advantage in coreAdvantages.advantages.slice(0, 3)" :key="advantage.title" class="card">
          <h3>{{ advantage.title }}</h3>
          <p>{{ advantage.description }}</p>
        </div>
      </div>
      <div class="grid-3" style="margin-top:18px">
        <div v-for="advantage in coreAdvantages.advantages.slice(3)" :key="advantage.title" class="card">
          <h3>{{ advantage.title }}</h3>
          <p>{{ advantage.description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.grid-3 {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 18px;
}

@media (max-width: 768px) {
  .grid-3 {
    grid-template-columns: 1fr;
    gap: 12px;
  }
}

.card {
  background: var(--banana-card-bg, #161b22);
  border: 1px solid var(--banana-border-color, #30363d);
  border-radius: 16px;
  padding: 24px;
  transition: all 0.3s ease;
  height: 100%;
}

.card:hover {
  border-color: var(--banana-primary-yellow, #FFD700);
  box-shadow: 0 20px 25px -5px rgba(255, 215, 0, 0.1), 0 10px 10px -5px rgba(255, 215, 0, 0.04);
}

.card h3 {
  font-size: 20px;
  font-weight: 700;
  color: var(--banana-text-light, #f0f6fc);
  margin-bottom: 12px;
  line-height: 1.2;
}

.card p {
  font-size: 16px;
  line-height: 1.6;
  color: var(--banana-text-muted, #8b949e);
  margin: 0;
}
</style>
