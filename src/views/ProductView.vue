<template>
  <div class="p-2 max-w-[500px] h-auto">
    <!--Seen In Page-->
    <div v-if="seein_show" class="flex flex-col">
      <!--Previous Button-->
      <button
        @click="seeninSwitch()"
        class="self-start mb-4 rounded-md border border-gray-300 px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50"
      >
        <span>&#8592;</span> Previous
      </button>
      
      <!--Seen In Data-->
      <div class="container grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        <div v-for="d in seenin_data" :key="d.id" :class="{ 'col-span-3': d.type === 'cover' }">
            <img :src="d.image" />
        </div>
      </div>
    </div>
    <div v-else class="flex flex-col" v-if="data">
      <!--Product Page-->
      <img :src="data.image" />
      <b class="mt-5 text-xl">{{ data.title }}</b>
      <p class="mt-2 text-gray-800">{{ data.description }}</p>
      <div class="ml-auto mt-5">
        <button @click="showSeenIn()" class="text-sm rounded-md bg-blue-700 text-white hover:bg-blue-800">Seen In</button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';
import axios from 'axios';

interface Product {
  id: number
  type: string
  image: string
  title: string
  description: string
}

const data = ref<Product | null>(null);
const seenin_data = ref<Product[]>([]);
const seein_show = ref(false);
const props = defineProps({
  id: {
    type: Number,
    required: true,
  }
});

// load product data
onMounted(async () => {
  try {
    const response = await axios.get('/database/product.json?id='+props.id);
    data.value = response.data;
  } catch (error) {
    console.error('API fail:', error);
  }
});

// load seen in data
const showSeenIn = async () => {
  seein_show.value = true;
  
  if (seenin_data.value.length === 0) { // prevent ajax fetch data again
    try {
      if (!data.value) return;
      const response = await axios.get('/database/seenin.json?id=' + data.value.id);
      seenin_data.value = response.data;
    } catch (error) {
      console.error('Seen In API fail:', error);
    }
  }
};

// switch seen in
const seeninSwitch = () => {
  seein_show.value = !seein_show.value;
}
</script>