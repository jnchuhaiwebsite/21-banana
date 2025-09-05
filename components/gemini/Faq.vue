<script setup lang="ts">
import { ref } from 'vue'

const faq = {
  title: 'Gemini 2.5 Flash Image - Frequently Asked Questions',
  description: 'Find answers to common questions about Gemini 2.5 Flash Image and its capabilities.',
  questions: [
    {
      question: 'How is Gemini 2.5 Flash Image different from other image generation models?',
      answer: 'Gemini 2.5 Flash Image stands out with its exceptional speed and efficiency while maintaining superior quality output. This revolutionary AI model is particularly advantageous for scenarios requiring rapid iteration and large-scale generation, making it the preferred choice for professional workflows.'
    },
    {
      question: 'What technical background do I need to use Gemini 2.5 Flash Image?',
      answer: 'Gemini 2.5 Flash Image is designed for accessibility. We provide a user-friendly interface and simple APIs, making it easy to get started whether you\'re a beginner or an experienced developer. No advanced technical knowledge is required to begin using Gemini 2.5 Flash Image.'
    },
    {
      question: 'Who owns the rights to images generated with Gemini 2.5 Flash Image?',
      answer: 'When using Gemini 2.5 Flash Image, you typically have commercial usage rights for the images you generate. However, we recommend reviewing our terms of service for detailed information about specific usage rights and restrictions for Gemini 2.5 Flash Image outputs.'
    },
    {
      question: 'Is there a free trial available for Gemini 2.5 Flash Image?',
      answer: 'Yes! We offer free generation credits for new users to experience the full capabilities of Gemini 2.5 Flash Image before committing to a paid plan. This allows you to test the model\'s performance and quality with your specific use cases.'
    }
  ]
};

// 不需要折叠功能，直接显示所有答案
</script>

<template>
  <div class="py-16 sm:py-20">
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <div class="mx-auto max-w-4xl">
        <h2 class="text-4xl font-extrabold tracking-tight text-center mb-6 bg-gradient-to-r from-banana-primary-yellow to-banana-secondary-blue text-transparent bg-clip-text" style="line-height: 1.4;">
          {{ faq.title }}
        </h2>
        <p class="text-lg leading-7 text-banana-text-muted text-center mb-16 max-w-2xl mx-auto">
          {{ faq.description }}
        </p>
        <dl class="grid grid-cols-1 lg:grid-cols-2 gap-6">
          <div v-for="(item, index) in faq.questions" :key="item.question" class="group">
            <div class="bg-banana-card-bg border border-banana-border-color rounded-2xl p-6 hover:border-banana-primary-yellow transition-all duration-300 h-full">
              <dt class="mb-4">
                <h3 class="text-lg font-bold leading-6 text-banana-text-light">
                  {{ item.question }}
                </h3>
              </dt>
              <dd>
                <p class="text-sm leading-6 text-banana-text-muted">
                  {{ item.answer }}
                </p>
              </dd>
            </div>
          </div>
        </dl>
      </div>
    </div>
  </div>
</template>

