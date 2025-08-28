<template>
  <div class="bg-banana-dark-bg text-banana-text-light font-['Inter']">
    <Hero />
    <About />
    <div class="bg-banana-card-bg">
      <Features />
    </div>
    <WhyChooseUs />
    <!-- <Benefits /> -->
    <div class="bg-banana-card-bg">
      <Faq />
    </div>

  </div>
</template>

<script setup lang="ts">
import Hero from '~/components/banana/Hero.vue';
import About from '~/components/banana/About.vue';
import Features from '~/components/banana/Features.vue';
import WhyChooseUs from '~/components/banana/WhyChooseUs.vue';
import Faq from '~/components/banana/Faq.vue';
import { useSeo } from '~/composables/useSeo';

useSeo({
  title: 'Nano Banana AI | Image-to-Image Editing with Gemini 2.5',
  description: 'Discover Nano Banana AI for fast, seamless image creation and editing. Simple to use, versatile styles, and perfect for creators, designers, and businesses.'
})


  // 检查URL中是否有锚点，并执行滚动
  const scrollToAnchor = () => {
    if (window.location.hash) {
      const sectionId = window.location.hash.substring(1);
      
      let attempts = 0;
      const maxAttempts = 30; // 增加尝试次数以应对慢网络
      
      const interval = setInterval(() => {
        const element = document.getElementById(sectionId);
        if (element) {
          clearInterval(interval);
          const offset = 80; // 导航栏高度
          const elementPosition = element.getBoundingClientRect().top;
          const offsetPosition = elementPosition + window.scrollY - offset;
          window.scrollTo({
            top: offsetPosition,
            behavior: 'smooth'
          });
        } else {
          attempts++;
          if (attempts > maxAttempts) {
            clearInterval(interval);
            console.warn(`无法找到ID为 '${sectionId}' 的元素`);
          }
        }
      }, 100);
    }
  };

  scrollToAnchor();
</script>
