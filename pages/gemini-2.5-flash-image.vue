<template>
  <div class="bg-banana-dark-bg text-banana-text-light font-['Inter']">
    <HeroPreview />
    <!-- Your existing content -->
    <GeminiAbout />
    <GeminiCoreAdvantages />
    <GeminiPromptGuide />
    <GeminiUseCases />
    <GeminiFaq />
  </div>
</template>

<script setup lang="ts">
import HeroPreview from '~/components/gemini/HeroPreview.vue';
import GeminiAbout from '~/components/gemini/About.vue';
import GeminiCoreAdvantages from '~/components/gemini/CoreAdvantages.vue';
import GeminiPromptGuide from '~/components/gemini/PromptGuide.vue';
import GeminiUseCases from '~/components/gemini/UseCases.vue';
import GeminiFaq from '~/components/gemini/Faq.vue';

import { useSeo } from '~/composables/useSeo';

useSeo({
  title: 'Gemini 2.5 Flash Image | Google’s Latest AI Image Tool 2025',
  description: 'Gemini 2.5 Flash Image is Google’s newest 2025 AI image model. Generate fast, edit smarter, and save costs — ideal for creators, brands, and content teams.'
})
</script>

<style scoped>
/* Add any page-specific styles here */
</style>
