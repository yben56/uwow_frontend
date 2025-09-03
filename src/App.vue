<template>
  <MastheadComp />
  <HeaderComp />
  <NavComp />
  <router-view></router-view>
  <FooterComp />
</template>

<script>
import MastheadComp from '@/components/MastheadComp.vue'
import HeaderComp from './components/HeaderComp.vue';
import NavComp from './components/NavComp.vue';
import FooterComp from '@/components/FooterComp.vue'

export default {
  components: { MastheadComp, HeaderComp, NavComp, FooterComp },
  name: 'App'
}
</script>