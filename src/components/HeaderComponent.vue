<template>
    <header>
        <div class="title-container">
            <h1 class="main-title">Ominous Generator</h1>
            <p class="subtitle">Unveil the mysteries of fate</p>
        </div>
    </header>
</template>
<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'HeaderComponent',
});
</script>
<style scoped>
header {
    margin: 0 auto 3rem auto;
}

.title-container {
    text-align: center;
    margin-top: 30px;
}

.main-title {
    font-size: 2.5em;
    color: #333;
}

.subtitle {
    font-size: 1.2em;
    color: #666;
    margin-top: 10px;
}
</style>
