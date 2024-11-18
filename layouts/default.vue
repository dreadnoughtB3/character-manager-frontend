<script setup lang="ts">
import Header from '~/components/common/Header.vue';
</script>

<template>
  <div>
    <Header />
    <div class="flex justify-center min-h-screen pt-16 bg-discord-100">
      <slot />
    </div>
  </div>
</template>