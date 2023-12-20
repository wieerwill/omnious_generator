<template>
    <footer class="footer">
        <a href="https://github.com/wieerwill/" target="_blank">GitHub</a>
        <a href="https://wieerwill.de" target="_blank">WieErWill.de</a>
    </footer>
</template>
  
<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'FooterComponent'
});
</script>
  
<style scoped>
.footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  width: 90%;
  margin: 5rem auto 0 auto;
  background-color: #f8f8f87e;
  border-top: 1px solid #e7e7e7;
}

.footer a {
  flex: 1;
  text-align: center;
  margin: 0 10px;
  color: #e7e7e7;
  text-decoration: none;
}
</style>
  