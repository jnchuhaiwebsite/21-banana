<template>
  <div class="relative w-full overflow-hidden ">
    <div class="container mx-auto px-4 relative z-10 pt-8">
      
      <!-- 主布局：两列网格 -->
      <div class="flex flex-col md:flex-row gap-8 lg:gap-12 items-start justify-center">

        <!-- 左列：表单 -->
        <div class="w-full mx-auto md:mx-0 md:w-[45%] max-w-[720px] md:max-w-[560px] bg-banana-card-bg/80 backdrop-blur-sm rounded-3xl shadow-2xl border border-banana-border-color/50 p-6 flex flex-col gap-4">

          <!-- 图片上传 -->
          <div>
            <label for="image-upload" class="block text-lg font-semibold text-banana-text-light mb-2 flex justify-between items-center">
              <span>Upload Images (Up to 9) </span>
              <button @click="showUploadGuide = true" class="text-sm text-banana-primary-yellow hover:underline flex items-center gap-1">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.546-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
                Use hints
              </button>
            </label>
            <div class="w-full min-h-[150px] border-2 border-dashed border-banana-primary-yellow/60 rounded-xl p-4 hover:border-banana-primary-yellow transition-colors relative bg-banana-dark-bg">
              <input 
                type="file" 
                accept="image/jpeg,image/png,image/webp" 
                class="hidden" 
                ref="fileInput"
                multiple
                @change="handleImageUpload"
              />

              <div v-if="imagePreviews.length > 0" class="grid grid-cols-3 gap-4">
                <!-- Image Previews -->
                <div v-for="(preview, index) in imagePreviews" :key="index" class="relative group aspect-square">
                  <img 
                    :src="preview" 
                    class="w-full h-full object-cover rounded-lg cursor-pointer border-2"
                    :class="mainPreview === preview ? 'border-banana-primary-yellow' : 'border-transparent'"
                    alt="Image preview"
                    @click="selectForEditing(preview)"
                  />
                  <button 
                    @click.stop="removeSelectedImage(index)"
                    class="absolute -top-2 -right-2 p-1 bg-red-600 rounded-full hover:bg-red-700 transition-colors opacity-0 group-hover:opacity-100 z-10"
                  >
                    <svg class="h-4 w-4 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                  </button>
                </div>

                <!-- Upload Button -->
                <div 
                  v-if="imagePreviews.length < 9"
                  class="flex flex-col items-center justify-center gap-2 h-full cursor-pointer border-2 border-dashed border-banana-text-muted/50 rounded-lg hover:border-banana-primary-yellow aspect-square"
                  @click="handleImageUploadClick"
                >
                  <svg class="h-8 w-8 text-banana-text-muted" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
                  </svg>
                  <div class="text-center">
                    <p class="text-sm text-banana-text-muted">Add More</p>
                    <p class="text-xs text-banana-text-muted/70">({{ imagePreviews.length }}/9)</p>
                  </div>
                </div>
              </div>
              
              <div 
                v-else
                class="flex flex-col items-center justify-center gap-2 h-full cursor-pointer h-[120px]"
                @click="handleImageUploadClick"
              >
                <svg class="h-8 w-8 text-banana-text-muted" stroke="currentColor" fill="none" viewBox="0 0 48 48">
                  <path d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                </svg>
                <div class="text-center">
                  <p class="text-sm text-banana-text-muted">Click or drag image(s) here</p>
                  <p class="text-xs text-banana-text-muted/70 mt-1">JPEG, PNG, WEBP only. Max 10MB</p>
                </div>
              </div>
            </div>
          </div>

          <!-- 编辑提示 -->
          <div>
            <label for="prompt" class="block text-lg font-semibold text-banana-text-light mb-2 flex justify-between items-center">
              <span>Edit Instructions</span>
              <!-- <button @click="showPromptGuide = true" class="text-sm text-banana-primary-yellow hover:underline flex items-center gap-1">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.546-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
                Prompt Guide
              </button> -->
            </label>
            <textarea
              v-model="prompt"
              id="prompt"
              ref="promptInput"
              class="w-full border-2 border-dashed border-banana-primary-yellow/60 h-32 rounded-xl bg-gradient-to-b from-banana-dark-bg to-gray-900 border border-banana-border-color text-banana-text-light px-4 py-3 focus:ring-2 focus:ring-banana-primary-yellow focus:border-transparent transition placeholder-banana-text-muted/50 text-base resize-none"
              placeholder="Please provide a prompt describing the video you want to generate. Both Chinese and English are supported."
              @focus="withLoginCheck()"
            ></textarea>
          </div>

          <!-- 质量等级 -->

          
          <!-- 预设样式 -->
          <div class="preset-gallery pt-4">
            <p class="text-banana-text-muted text-center">get inspired by a preset style</p>
            <div class="grid grid-cols-2 gap-3 mt-4">
              <button
                v-for="preset in presets"
                :key="preset.name"
                @click="applyPreset(preset)"
                class="px-4 py-3 bg-banana-border-color/50 border-2 border-banana-border-color rounded-lg text-banana-text-light hover:bg-banana-primary-yellow hover:text-banana-dark-bg hover:border-banana-primary-yellow transition-colors text-sm text-center"
              >
                <span class="font-semibold">{{ preset.name }}</span>
              </button>
            </div>
          </div>
          
          <!-- 编辑按钮 -->
          <button @click="editImage" :disabled="loading || !mainPreview" class="relative w-full flex items-center justify-center gap-2 px-4 mt-6 lg:px-6 py-3 sm:py-4 bg-banana-primary-yellow/80 text-banana-dark-bg hover:bg-banana-primary-yellow rounded-full font-extrabold text-base sm:text-lg lg:text-xl shadow-xl transition transform hover:-translate-y-1 disabled:opacity-50 disabled:cursor-not-allowed">
            <svg v-if="loading" class="animate-spin -ml-1 mr-3 h-5 w-5 text-banana-dark-bg" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
              <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
              <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
            </svg>
            <span v-if="loading">Generate...</span>
            <span v-else>✨ Generate Image</span>
            <span class="absolute -top-2 -right-2 bg-banana-secondary-blue text-white text-xs font-bold px-2 py-1 rounded-full shadow-lg border-2 border-white/50">{{credit}} credit</span>
          </button>
        </div>

        <!-- 右列：预览 -->
        <div class="w-full  mx-auto md:mx-0 md:w-[55%] max-w-[720px] bg-banana-card-bg/50 backdrop-blur-sm rounded-3xl shadow-2xl border border-banana-border-color/50 p-4 overflow-hidden flex flex-col justify-center">
          <div class="w-full flex justify-end mb-4">
            <!-- 下载按钮 -->
            <button 
              v-if="previewImage && !loading" 
              @click="downloadImage" 
              class="bg-gradient-to-r from-banana-primary-yellow to-banana-secondary-blue text-banana-dark-bg font-bold py-2 px-4 rounded-full shadow-lg hover:shadow-xl transition-all duration-300 transform hover:scale-105 flex items-center gap-2"
              :disabled="downLoading"
            >
              <svg 
                v-if="!downLoading" 
                xmlns="http://www.w3.org/2000/svg" 
                class="h-5 w-5" 
                fill="none" 
                viewBox="0 0 24 24" 
                stroke="currentColor"
              >
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
              </svg>
              <svg 
                v-else 
                class="animate-spin h-5 w-5" 
                xmlns="http://www.w3.org/2000/svg" 
                fill="none" 
                viewBox="0 0 24 24"
              >
                <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
              </svg>
              <span>{{ downLoading ? 'Downloading...' : 'Download' }}</span>
            </button>
          </div>
          <!-- 固定高度的图片容器 -->
          <div class="w-full border-2 border-dashed border-banana-primary-yellow/60 h-[500px] md:h-[550px] lg:h-[645px] flex items-center justify-center bg-banana-dark-bg/50 rounded-2xl">
                       <!-- 原始图片 -->
            <img v-if="mainPreview && !previewImage" :src="mainPreview" class="max-w-full max-h-full object-contain rounded-lg transition-opacity duration-300" :class="{'opacity-50': loading}" alt="Nano Bananan Original Image"/>
                       <!-- 编辑后的图片 -->
            <img v-else-if="previewImage" :src="previewImage" class="max-w-full max-h-full object-contain rounded-lg transition-opacity duration-300" :class="{'opacity-50': loading}" alt="Nano Banana Edited Image"/>

          </div>

          <!-- Demo Text -->
          <div v-if="!previewImage" class="absolute bottom-8 left-1/2 -translate-x-1/2 bg-black/60 text-white text-base px-5 py-2.5 rounded-full pointer-events-none shadow-lg">
            Nano Banana AI Generation Demo
          </div>

          <!-- 加载覆盖层 -->
          <div v-if="loading" class="absolute inset-0 flex flex-col items-center justify-center bg-gradient-to-b from-banana-dark-bg to-gray-900/50 rounded-lg">
              <svg class="animate-spin h-10 w-10 text-banana-primary-yellow" xmlns="http://www.w.org/2000/svg" fill="none" viewBox="0 0 24 24">
                <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
              </svg>
              <p class="text-white mt-4 text-lg">Creating your masterpiece with Nano Banana AI...</p>
          </div>


        </div>

      </div>
    </div>
    
    <!-- Prompt Guide Modal -->
    <div v-if="showPromptGuide" class="fixed inset-0 bg-black bg-opacity-75 flex items-center justify-center z-50 p-4">
      <div class="bg-banana-dark-bg rounded-2xl shadow-xl w-full max-w-2xl border border-banana-border-color/50 overflow-hidden">
        <div class="p-6 border-b border-banana-border-color/50 flex justify-between items-center">
          <h3 class="text-2xl font-bold text-white">Prompt Guide</h3>
          <button @click="showPromptGuide = false" class="text-banana-text-muted hover:text-white">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
        <div class="p-8">
          <div class="space-y-6">
            <!-- Item 1: Prompt Length -->
            <div class="flex items-start gap-4">
              <div class="flex-shrink-0 w-10 h-10 flex items-center justify-center rounded-lg bg-banana-primary-yellow/10 text-banana-primary-yellow">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                </svg>
              </div>
              <div>
                <h4 class="font-bold text-white text-lg">Prompt Length</h4>
                <p class="text-banana-text-muted">Keep prompts under 120 characters for optimal results.</p>
              </div>
            </div>

            <!-- Item 2: Language -->
            <div class="flex items-start gap-4">
              <div class="flex-shrink-0 w-10 h-10 flex items-center justify-center rounded-lg bg-banana-primary-yellow/10 text-banana-primary-yellow">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
                </svg>
              </div>
              <div>
                <h4 class="font-bold text-white text-lg">Language</h4>
                <p class="text-banana-text-muted">Use simple, natural language for your instructions.</p>
              </div>
            </div>

            <!-- Item 3: Clarity -->
            <div class="flex items-start gap-4">
              <div class="flex-shrink-0 w-10 h-10 flex items-center justify-center rounded-lg bg-banana-primary-yellow/10 text-banana-primary-yellow">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
                </svg>
              </div>
              <div>
                <h4 class="font-bold text-white text-lg">Clarity</h4>
                <p class="text-banana-text-muted">For better accuracy, provide one clear instruction per edit.</p>
              </div>
            </div>

            <!-- Item 4: Specificity -->
            <div class="flex items-start gap-4">
              <div class="flex-shrink-0 w-10 h-10 flex items-center justify-center rounded-lg bg-banana-primary-yellow/10 text-banana-primary-yellow">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                  <path stroke-linecap="round" stroke-linejoin="round" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                </svg>
              </div>
              <div>
                <h4 class="font-bold text-white text-lg">Specificity</h4>
                <p class="text-banana-text-muted">When editing a specific area, precisely describe the target and the desired change.</p>
              </div>
            </div>
            
            <!-- Item 5: Edit Strength -->
            <div class="flex items-start gap-4">
              <div class="flex-shrink-0 w-10 h-10 flex items-center justify-center rounded-lg bg-banana-primary-yellow/10 text-banana-primary-yellow">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M12 6V4m0 16v-2m0-8v-2m0 4h.01M6 12H4m16 0h-2m-8 0h.01M12 18h.01M18 12h.01M6 12h.01M12 6h.01M18 6L6 18" />
                </svg>
              </div>
              <div>
                <h4 class="font-bold text-white text-lg">Edit Strength</h4>
                <p class="text-banana-text-muted">If the effect is too subtle, increase the 'scale' value for a stronger impact.</p>
              </div>
            </div>

            <!-- Item 6: Image Quality -->
            <div class="flex items-start gap-4">
              <div class="flex-shrink-0 w-10 h-10 flex items-center justify-center rounded-lg bg-banana-primary-yellow/10 text-banana-primary-yellow">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z" />
                </svg>
              </div>
              <div>
                <h4 class="font-bold text-white text-lg">Image Quality</h4>
                <p class="text-banana-text-muted">Start with clear, high-resolution images for the best outcomes.</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Upload Guide Modal -->
    <div v-if="showUploadGuide" class="fixed inset-0 bg-black bg-opacity-75 flex items-center justify-center z-50 p-4">
      <div class="bg-banana-dark-bg rounded-2xl shadow-xl w-full max-w-2xl border border-banana-border-color/50 overflow-hidden">
        <div class="p-6 border-b border-banana-border-color/50 flex justify-between items-center">
          <h3 class="text-2xl font-bold text-white">Use hints</h3>
          <button @click="showUploadGuide = false" class="text-banana-text-muted hover:text-white">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
        <div class="p-8">
          <div class="space-y-6">
            <!-- Item 1: Language -->
            <div class="flex items-start gap-4">
              <div class="flex-shrink-0 w-10 h-10 flex items-center justify-center rounded-lg bg-banana-primary-yellow/10 text-banana-primary-yellow">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M21 12a9 9 0 01-9 9m9-9a9 9 0 00-9-9m9 9H3m9 9a9 9 0 01-9-9m9 9V3m0 18a9 9 0 009-9m-9 9a9 9 0 00-9-9" />
                </svg>
              </div>
              <div>
                <h4 class="font-bold text-white text-lg">Language Performance</h4>
                <p class="text-banana-text-muted">Nano Banana AI supports English, Spanish, Japanese, Chinese, and Hindi. For the best performance, please use English.</p>
              </div>
            </div>

            <!-- Item 2: Image Count -->
            <div class="flex items-start gap-4">
              <div class="flex-shrink-0 w-10 h-10 flex items-center justify-center rounded-lg bg-banana-primary-yellow/10 text-banana-primary-yellow">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zM14 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z" />
                </svg>
              </div>
              <div>
                <h4 class="font-bold text-white text-lg">Optimal Image Count</h4>
                <p class="text-banana-text-muted">The model works best when you upload up to 3 images.</p>
              </div>
            </div>

            <!-- Item 3: Text in Image -->
            <div class="flex items-start gap-4">
              <div class="flex-shrink-0 w-10 h-10 flex items-center justify-center rounded-lg bg-banana-primary-yellow/10 text-banana-primary-yellow">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M7 8h10M7 12h4m1 8l-4-4H5a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v8a2 2 0 01-2 2h-3l-4 4z" />
                </svg>
              </div>
              <div>
                <h4 class="font-bold text-white text-lg">Text Within Images</h4>
                <p class="text-banana-text-muted">When generating text within an image, it’s recommended to first generate the text and then request an image containing that text.</p>
              </div>
            </div>

            <!-- Item 4: Child Safety -->
            <div class="flex items-start gap-4">
              <div class="flex-shrink-0 w-10 h-10 flex items-center justify-center rounded-lg bg-banana-primary-yellow/10 text-banana-primary-yellow">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M18.364 18.364A9 9 0 005.636 5.636m12.728 12.728A9 9 0 015.636 5.636m12.728 12.728L5.636 5.636" />
                </svg>
              </div>
              <div>
                <h4 class="font-bold text-white text-lg">Child Safety Policy</h4>
                <p class="text-banana-text-muted">Uploading photos of children is not supported in the European Economic Area (EEA), Switzerland (CH), or the United Kingdom (UK).</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, nextTick, onMounted } from 'vue';
import { useUserStore } from '~/stores/user';
import { useUiStore } from '~/stores/ui';
import { useRouter } from 'vue-router';
import { editImage as editImageApi, upload } from '~/api';
import { useNuxtApp } from 'nuxt/app';
const { $toast } = useNuxtApp() as any;
const showPromptGuide = ref(false);
const showUploadGuide = ref(false);

const credit = ref(1);

interface ImageResponse {
  code: number;
  msg: string;
  data?: {
    task_id: string;
    image_url: string;
  };
  success: boolean;
}

const router = useRouter()

interface Preset {
  name: string;
  prompt: string;
}

const userStore = useUserStore();
const uiStore = useUiStore();

const userInfo = computed(() => userStore.userInfo);

const withLoginCheck = async (callback?: () => void | Promise<void>) => {
  const isLoggedIn = await checkLoginStatus();
  if (isLoggedIn && callback) {
    await callback();
  }
};

const checkLoginStatus = async () => {
  if (!userInfo.value) {
    uiStore.showLoginPrompt();
    return false;
  }
  return true;
};

const prompt = ref('');
const promptInput = ref<HTMLTextAreaElement | null>(null);
const selectedImages = ref<File[]>([]);
const imagePreviews = ref<string[]>([]);
const mainPreview = ref<string>('https://resp.nano-banana-ai.net/nano/images/nano-banana-ai.webp');
const fileInput = ref<HTMLInputElement | null>(null);

const qualityLevel = ref(3);

// 计算滑块的进度百分比
const qualityProgress = computed(() => {
  const min = 1;
  const max = 5;
  const value = qualityLevel.value;
  return ((value - min) / (max - min)) * 100;
});

const updateQualityProgress = () => {
  // 强制重新计算样式
  nextTick(() => {
    const slider = document.getElementById('quality') as HTMLInputElement;
    if (slider) {
      slider.style.setProperty('--range-progress', qualityProgress.value + '%');
    }
  });
};

const loading = ref(false);
const downLoading = ref(false);
const previewImage = ref<string>('');

const presets = [
  {
    name: 'Add and remove elements',
    prompt: 'Using the provided image of [subject], please [add/remove/modify] [element] to/from the scene. Ensure the change is [description of how the change should integrate].'
  },
  {
    name: 'Partial redraw / Local repaint',
    prompt: 'Using the provided image, change only the [specific element] to [new element/description]. Keep everything else in the image exactly the same,preserving the original style, lighting, and composition.'
  },
  {
    name: 'Style transfer',
    prompt: 'Transform the provided photograph of [subject] into the artistic style of [artist/art style]. Preserve the original composition but render it with [description of stylistic elements].' // 优化：更简洁，“style”已足够清晰
  },
  {
    name: 'Combine multiple images',
    prompt: 'Create a new image by combining the elements from the provided images. Take the [element from image 1] and place it with/on the [element from image 2]. The final image should be a [description of the final scene].' 
  }
];



// 处理图片上传区域点击
const handleImageUploadClick = async () => {
  if (!await checkLoginStatus()) return
  fileInput.value?.click()
}

// 校验并处理单个图片文件
const validateAndProcessImage = (file: File): Promise<{ file: File; previewUrl: string } | null> => {
  return new Promise((resolve) => {
    // 1. 检查图片格式
    const allowedTypes = ['image/jpeg', 'image/png', 'image/webp'];
    if (!allowedTypes.includes(file.type)) {
      $toast.error(`Unsupported format for ${file.name}. Please use JPEG or PNG.`);
      resolve(null);
      return;
    }

    // 2. 检查图片大小
    if (file.size > 10 * 1024 * 1024) { // 10MB
      $toast.error(`Image ${file.name} is too large (max 10MB).`);
      resolve(null);
      return;
    }

    // 3. 检查图片尺寸和宽高比
    const reader = new FileReader();
    reader.onload = (e) => {
      const img = new Image();
      img.onload = () => {
        const { width, height } = img;

        if (width <= 14 || height <= 14) {
          $toast.error(`Image dimensions for ${file.name} must be greater than 14px.`);
          resolve(null);
          return;
        }

        const aspectRatio = width / height;
        if (aspectRatio <= 1 / 3 || aspectRatio >= 3) {
          $toast.error(`Image aspect ratio for ${file.name} must be between 1/3 and 3.`);
          resolve(null);
          return;
        }

        // 所有检查通过
        resolve({
          file: file,
          previewUrl: URL.createObjectURL(file),
        });
      };
      img.onerror = () => {
        $toast.error(`Failed to load image ${file.name}, it may be corrupted.`);
        resolve(null);
      };
      img.src = e.target?.result as string;
    };
    reader.onerror = () => {
      $toast.error(`Failed to read file ${file.name}.`);
      resolve(null);
    };
    reader.readAsDataURL(file);
  });
};


// 处理图片上传
const handleImageUpload = async (event: Event) => {
  const input = event.target as HTMLInputElement;
  if (!input.files?.length) return;

  const files = Array.from(input.files);

  if (selectedImages.value.length + files.length > 9) {
    $toast.error('You can upload up to 9 images.');
    if (input) {
      input.value = '';
    }
    return;
  }

  for (const file of files) {
    if (selectedImages.value.length >= 9) {
        $toast.info('Reached the maximum of 9 images.');
        break;
    }
    const result = await validateAndProcessImage(file);
    if (result) {
      selectedImages.value.push(result.file);
      imagePreviews.value.push(result.previewUrl);
    }
  }
  
  // 如果当前没有主预览图，则默认选择第一张上传的图片
  // if (imagePreviews.value.length > 0 && mainPreview.value === 'https://resp.nano-banana-ai.net/nano/images/nano-banana-ai.webp') {
  //   mainPreview.value = imagePreviews.value[0];
  // }

  if (input) {
    input.value = '';
  }
};

// 移除已选择的图片
const removeSelectedImage = (index: number) => {
  const removedPreview = imagePreviews.value[index];
  URL.revokeObjectURL(removedPreview);
  
  selectedImages.value.splice(index, 1);
  imagePreviews.value.splice(index, 1);

  // 如果被删除的图片是当前主预览图
  if (mainPreview.value === removedPreview) {
    mainPreview.value = 'https://resp.nano-banana-ai.net/nano/images/nano-banana-ai.webp';
    previewImage.value = '';
  }
};

const selectForEditing = (previewUrl: string) => {
  mainPreview.value = previewUrl;
}

const applyPreset = (preset: Preset) => {
  prompt.value = preset.prompt;
};

const editImage = async () => {
  if (selectedImages.value.length === 0) {
    $toast.error('Please upload an image first');
    return;
  }

  if (!prompt.value.trim()) {
    $toast.error('Please enter edit instructions');
    return;
  }
  await userStore.fetchUserInfo(true); // Force refresh user info
  const remainingTimes = computed(() => userStore.userInfo?.free_limit + userStore.userInfo?.remaining_limit || 0)
  // 检查使用限制
  const checkUsageLimit = () => {
    if (remainingTimes.value < credit.value) {
      $toast.info('Usage limit reached. Please upgrade to premium for more credits');
      router.push('/pricing')
      return false
    }
    return true
  }
  if (!checkUsageLimit()) {
    return;
  }

  loading.value = true;
  
  try {
    const uploadedUrls: string[] = [];

    // 1. 如果有用户上传的图片，则依次上传它们
    if (selectedImages.value.length > 0) {
      // $toast.info(`Uploading ${selectedImages.value.length} image(s)...`);
      for (const file of selectedImages.value) {
        try {
          const formData = { file };
          const response = await upload(formData);
          if (response.data && typeof response.data === 'string') {
            uploadedUrls.push(response.data);
          } else {
            throw new Error('Invalid response from upload server.');
          }
        } catch (uploadError) {
          throw new Error(`Failed to upload ${file.name}.`);
        }
      }
    }
    
    // 使用 || 拼接URL
    const img_urls = uploadedUrls.join('||');
    
    // 准备请求参数
    const requestData = {
      img_urls,
      prompt: prompt.value.trim(),
    };
    
    // 调用editImage API
    const result = await editImageApi(requestData) as ImageResponse;
    
    if (result.code !== 200 || !result.success || !result.data?.image_url) {
      throw new Error(result.msg || '图片编辑失败');
    }
    
    // 显示编辑后的图片
    previewImage.value = result.data.image_url;
    
    $toast.success('Image edited successfully!');
    // Deduct credit on frontend for immediate feedback, backend should be the source of truth
    if(userStore.userInfo) {
      userStore.userInfo.credits -= 1;
    }
  } catch (error: any) {
    $toast.error(error.message || 'Failed to edit image');
    console.error('编辑图片失败:', error);
  } finally {
    loading.value = false;
  }
};

async function downloadImage() {
  if (previewImage.value) {
    try {
      // 开始下载时显示加载状态
      downLoading.value = true;
      
      // 获取图片数据
      const response = await fetch(previewImage.value);
      const blob = await response.blob();
      
      // 创建 blob URL
      const blobUrl = window.URL.createObjectURL(blob);
      
      // 创建一个临时的 a 标签
      const link = document.createElement('a');
      link.href = blobUrl;
      // 设置文件名
      const fileName = 'nano-banana.png';
      link.download = fileName;
      
      // 触发下载
      document.body.appendChild(link);
      link.click();
      
      // 清理
      document.body.removeChild(link);
      window.URL.revokeObjectURL(blobUrl);
      
      $toast.success('Image downloaded successfully!');
    } catch (error) {
      console.error('Download error:', error);
      $toast.error('Download failed, please try again later');
    } finally {
      downLoading.value = false;
    }
  }
};

onMounted(() => {
  // 组件挂载时初始化滑块样式
  nextTick(() => {
    updateQualityProgress();
  });
});
</script>

<style scoped>
/* 重置滑块的基础样式 */
input[type="range"] {
  -webkit-appearance: none;
  appearance: none;
  background: linear-gradient(to right, #FFD700 0%, #FFD700 var(--range-progress), #374151 var(--range-progress), #374151 100%);
  border-radius: 8px;
  height: 8px;
  outline: none;
}

input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #FFD700;
  cursor: pointer;
  box-shadow: 0 2px 6px rgba(255, 215, 0, 0.3);
}

input[type="range"]::-moz-range-thumb {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #FFD700;
  cursor: pointer;
  border: none;
  box-shadow: 0 2px 6px rgba(255, 215, 0, 0.3);
}
</style>
