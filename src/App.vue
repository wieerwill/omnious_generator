<template>
  <div id="app">
    <header-component />
    <ominous-generator />
    <footer-component />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import HeaderComponent from './components/HeaderComponent.vue';
import FooterComponent from './components/FooterComponent.vue';
import OminousGenerator from './components/OmniousGenerator.vue';

export default defineComponent({
  name: 'App',
  components: {
    HeaderComponent,
    FooterComponent,
    OminousGenerator
  }
});
</script>
<style></style>
