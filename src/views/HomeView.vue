<template>
  <div class="container mt-10 mx-auto lg:max-w-screen-lg grid">
    <div v-for="d in data" :key="d.id" :class="{ 'col-span-3': d.type === 'cover' }">
        <ModalComp template="product" title="Product Detail">
          <template v-slot:body-content>
              <ProductView :id="d.id" />
          </template>
          <template v-slot:toggle-btn="{ openModal }">
            <img :src="d.image" @click="openModal" class="cursor-pointer"/>
          </template>
        </ModalComp>
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';
import ModalComp from '@/components/ModalComp.vue';
import ProductView from '@/views/ProductView.vue';
import axios from 'axios';

const data = ref('')

onMounted(async () => {
  try {
    const response = await axios.get('/database/products.json');
    data.value = response.data;
  } catch (error) {
    console.error('API fail:', error);
  }
});
</script>