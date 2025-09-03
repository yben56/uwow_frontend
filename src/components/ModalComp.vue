<template>
  <div>
    <div :id="template" class="fixed inset-0 z-50 overflow-y-auto bg-black bg-opacity-50 transition-opacity duration-300 ease-out" v-if="isOpen">
      <div class="flex items-center justify-center p-4 min-h-screen">
        <div class="bg-white rounded-md shadow-lg overflow-hidden transition-all duration-300 ease-out transform scale-95" ref="modalContentRef">
          
          <div class="px-5 py-3 border-b flex items-center justify-between">
            <h5 class="text-lg font-semibold text-gray-800">{{ title }}</h5>
            <button type="button" class="modal-close-button text-gray-500 hover:text-gray-700 transition ms-2" @click="closeModal" aria-label="Close">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
          </div>

          <div class="p-5">
            <slot name="body-content"></slot>
          </div>
        </div>
      </div>
    </div>
    
    <slot name="toggle-btn" :openModal="openModal"></slot>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  template: {
    type: String,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
});

const isOpen = ref(false);

const openModal = () => {
  isOpen.value = true;
};

const closeModal = () => {
  isOpen.value = false;
};
</script>

<style scoped>
.modal-close-button:hover {
  box-shadow: none !important;
}
</style>