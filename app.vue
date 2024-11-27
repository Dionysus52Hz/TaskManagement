<template>
   <NuxtLayout>
      <NuxtPage />
   </NuxtLayout>
</template>

<script setup lang="ts">
   useHead({
      title: 'Schedule App',
      meta: [{ name: 'description', content: 'My amazing site.' }],
      bodyAttrs: {
         class: 'test',
      },
   });
</script>
