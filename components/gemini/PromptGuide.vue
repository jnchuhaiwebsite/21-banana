<script setup lang="ts">
import { ref } from 'vue'

const promptGuide = {
  title: 'Gemini 2.5 Flash Image - Prompt Guide',
  description: 'Master the art of prompt engineering to unlock the full potential of Gemini 2.5 Flash Image.',
  categories: [
  {
      type: 'Photorealistic scenes',
      description: 'Create stunning photorealistic images using professional photography terminology. Specify camera settings, lens types, lighting conditions, and composition details for maximum realism and visual impact.',
      template: 'A photorealistic [shot type: close-up/medium shot/wide shot] of [subject], [action or expression], set in [environment]. The scene is illuminated by [lighting: natural/studio/golden hour/blue hour], creating a [mood: serene/dramatic/mysterious/energetic] atmosphere. Captured with a [camera: DSLR/mirrorless] and [lens: 24mm/50mm/85mm/200mm], emphasizing [textures: skin texture/fabric details/surface materials]. The image should be in [aspect ratio: 16:9/4:3/1:1/portrait] format with [depth of field: shallow/deep] focus.',
      example: 'A photorealistic close-up portrait of an elderly Japanese ceramicist with deep, sun-etched wrinkles and a warm, knowing smile. He is carefully inspecting a freshly glazed tea bowl with weathered hands. The setting is his rustic, sun-drenched workshop with clay dust particles floating in the air. The scene is illuminated by soft, golden hour light streaming through a window, creating dramatic shadows and highlighting the fine texture of the clay. Captured with a DSLR camera and 85mm portrait lens, resulting in a soft, blurred background (bokeh) with shallow depth of field. The overall mood is serene and masterful. Vertical portrait orientation in 4:3 aspect ratio.'
    },
    {
      type: 'Stylized illustrations & stickers',
      description: 'Design eye-catching stickers, icons, and digital assets with specific artistic styles. Perfect for social media, apps, and branding materials with clean, scalable designs.',
      template: 'A [style: kawaii/flat design/line art/watercolor/vector] sticker of a [subject], featuring [characteristics: expression/pose/accessories] and a [color palette: vibrant/muted/monochrome/pastel]. The design should have [line style: bold/clean/thin/rough] and [shading: cel-shading/flat colors/gradient/no shading]. The background must be [background: transparent/white/solid color].',
      example: 'A kawaii-style sticker of a happy red panda wearing a tiny bamboo hat with a cute expression and playful pose. It\'s munching on a green bamboo leaf with its paws. The design features bold, clean outlines, simple cel-shading with soft gradients, and a vibrant color palette of red, green, and brown tones. The background must be transparent for easy integration into any design.'
    },
    {
      type: 'Accurate text in images',
      description: 'Create professional designs with accurate text rendering. Perfect for logos, posters, banners, and business materials where typography is crucial for brand identity and communication.',
      template: 'Create a [image type: logo/poster/banner/business card] for [brand/concept] with the text "[text to render]" in a [font style: serif/sans-serif/script/display]. The design should be [style: minimalist/modern/vintage/playful/professional], with a [color scheme: monochrome/duotone/triadic/complementary]. Include [additional elements: icons/illustrations/patterns/borders].',
      example: 'Create a modern, minimalist logo for a coffee shop called \'The Daily Grind\' with the text rendered in a clean, bold, sans-serif font. The design should feature a simple, stylized coffee bean icon seamlessly integrated with the text. The style should be professional and contemporary, with a monochrome color scheme of black and white. Include subtle geometric patterns as additional elements to enhance the overall design.'
    },
    {
      type: 'Product mockups & commercial photography',
      description: 'Create high-quality commercial product photography with professional lighting and composition. Ideal for e-commerce, marketing campaigns, and brand materials that require premium visual presentation.',
      template: 'A high-resolution, studio-lit product photograph of a [product: electronics/fashion/food/beverage/beauty] on a [background: marble/wood/concrete/fabric/paper]. The lighting is a [lighting setup: three-point/ring light/softbox/rim lighting] to [purpose: highlight texture/create shadows/showcase form]. The camera angle is a [angle: 45-degree/overhead/eye-level/low angle] to showcase [feature: texture/logo/functionality/scale]. Ultra-realistic, with sharp focus on [detail: product name/logo/texture/reflection]. [Aspect ratio: 16:9/4:3/1:1/square].',
      example: 'A high-resolution, studio-lit product photograph of a minimalist ceramic coffee mug in matte black, presented on a polished concrete surface. The lighting is a three-point softbox setup designed to highlight texture and create soft, diffused highlights while eliminating harsh shadows. The camera angle is a slightly elevated 45-degree shot to showcase its clean lines and ergonomic design. Ultra-realistic, with sharp focus on the steam rising from the coffee and the subtle texture of the ceramic surface. Square image in 1:1 aspect ratio.'
    },
    {
      type: 'Minimalist & negative space design',
      description: 'Design clean, minimalist compositions with strategic use of negative space. Perfect for website backgrounds, presentation slides, and marketing materials that require text overlay and visual breathing room.',
      template: 'A minimalist composition featuring a single [subject: object/person/plant/geometric shape] positioned in the [position: bottom-right/top-left/center/rule of thirds] of the frame. The background is a vast, empty [color: white/off-white/light gray/pastel] canvas, creating significant negative space for [purpose: text overlay/logo placement/breathing room]. Soft, subtle lighting from [direction: top-left/top-right/side/back]. [Aspect ratio: 16:9/4:3/1:1/portrait/landscape].',
      example: 'A minimalist composition featuring a single, delicate red maple leaf positioned in the bottom-right of the frame using the rule of thirds. The background is a vast, empty off-white canvas, creating significant negative space for text overlay and logo placement. Soft, diffused lighting from the top-left direction creates subtle shadows and depth. Square image in 1:1 aspect ratio, perfect for social media and web backgrounds.'
    },
    {
      type: 'Sequential art (Comic panel / Storyboard)',
      description: 'Create compelling comic panels and storyboards with consistent character design and dynamic storytelling. Perfect for graphic novels, storyboards, and sequential art projects that require narrative flow and visual impact.',
      template: 'A single comic book panel in a [art style: manga/american/indie/noir/superhero] style. In the foreground, [character: description/pose/expression/action]. In the background, [setting: location/atmosphere/weather/time of day]. The panel has a [text element: speech bubble/thought bubble/caption box/narration] with the text "[Text]". The lighting creates a [mood: dramatic/suspenseful/comedic/romantic] mood. [Aspect ratio: 16:9/4:3/1:1/portrait/landscape].',
      example: 'A single comic book panel in a gritty, noir art style with high-contrast black and white inks. In the foreground, a detective in a trench coat stands under a flickering streetlamp with a determined expression and confident pose, rain soaking his shoulders. In the background, the neon sign of a desolate bar reflects in a puddle during a dark, stormy night. A caption box at the top reads "The city was a tough place to keep secrets." The lighting is harsh and dramatic, creating a suspenseful and somber mood. Landscape orientation in 16:9 aspect ratio.'
    },
  ]
};

const activeTab = ref<number>(0)
const showTemplate = ref<boolean>(true)

const toggleView = () => {
  showTemplate.value = !showTemplate.value
}

const copyToClipboard = async (text: string) => {
  try {
    await navigator.clipboard.writeText(text)
    // 可以添加一个toast通知
    console.log('Copied to clipboard!')
  } catch (err) {
    console.error('Failed to copy: ', err)
  }
}
</script>

<template>
  <div class="py-16 sm:py-20">
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <div class="mx-auto max-w-4xl text-center mb-16">
        <h2 class="text-4xl font-extrabold tracking-tight sm:text-5xl lg:text-6xl bg-gradient-to-r from-banana-primary-yellow to-banana-secondary-blue text-transparent bg-clip-text">
          {{ promptGuide.title }}
        </h2>
        <p class="mt-6 text-lg leading-7 text-banana-text-muted max-w-2xl mx-auto">
          {{ promptGuide.description }}
        </p>
      </div>
      <!-- Category Tabs -->
      <div class="flex flex-wrap justify-center gap-2 mb-8">
        <button
          v-for="(category, index) in promptGuide.categories"
          :key="category.type"
          @click="activeTab = index"
          :class="[
            'px-4 py-2 rounded-lg text-sm font-medium transition-all duration-200',
            activeTab === index
              ? 'bg-gradient-to-r from-banana-primary-yellow to-banana-secondary-blue text-banana-dark-bg'
              : 'bg-banana-card-bg border border-banana-border-color text-banana-text-muted hover:border-banana-primary-yellow hover:text-banana-text-light'
          ]"
        >
          {{ category.type }}
        </button>
      </div>

      <!-- Active Category Content -->
      <div class="bg-banana-card-bg border border-banana-border-color rounded-2xl p-8">
        <div class="mb-6">
          <h3 class="text-2xl font-bold text-banana-text-light mb-3">
            {{ promptGuide.categories[activeTab].type }}
          </h3>
          <p class="text-lg text-banana-text-muted">
            {{ promptGuide.categories[activeTab].description }}
          </p>
        </div>


        <!-- Content Display -->
        <div class="bg-banana-dark-bg border border-banana-border-color rounded-xl p-6">
          <!-- Tab Labels -->
          <div class="flex gap-1 mb-4">
            <button
              @click="showTemplate = true"
              :class="[
                'px-3 py-2 rounded-lg text-sm font-medium transition-all duration-200',
                showTemplate
                  ? 'bg-gradient-to-r from-banana-primary-yellow to-banana-secondary-blue text-banana-dark-bg'
                  : 'bg-banana-card-bg border border-banana-border-color text-banana-text-muted hover:border-banana-primary-yellow hover:text-banana-text-light'
              ]"
            >
              Template
            </button>
            <button
              @click="showTemplate = false"
              :class="[
                'px-3 py-2 rounded-lg text-sm font-medium transition-all duration-200',
                !showTemplate
                  ? 'bg-gradient-to-r from-banana-primary-yellow to-banana-secondary-blue text-banana-dark-bg'
                  : 'bg-banana-card-bg border border-banana-border-color text-banana-text-muted hover:border-banana-primary-yellow hover:text-banana-text-light'
              ]"
            >
              Prompt
            </button>
          </div>

          <!-- Content with Copy Button -->
          <div class="bg-banana-card-bg rounded-lg p-4 relative">
            <button
              @click="copyToClipboard(showTemplate ? promptGuide.categories[activeTab].template : promptGuide.categories[activeTab].example)"
              class="absolute top-3 right-3 p-2 text-banana-text-muted hover:text-banana-primary-yellow transition-colors duration-200 rounded-lg hover:bg-banana-dark-bg/50"
              title="Copy to clipboard"
            >
              <svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"></path>
              </svg>
            </button>
            <p class="text-banana-primary-yellow font-mono text-sm leading-relaxed pr-16">
              {{ showTemplate ? promptGuide.categories[activeTab].template : promptGuide.categories[activeTab].example }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
