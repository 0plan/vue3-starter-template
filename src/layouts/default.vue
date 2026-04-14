<script setup lang="ts">
import Footer from '~/components/Footer.vue'
</script>

<template>
  <main class="flex flex-col min-h-screen bg-background text-foreground">
    <Header />
    <div class="flex-grow pt-20 px-4 py-10 w-full max-w-7xl mx-auto">
      <RouterView />
    </div>
    <div class="text-center pb-6">
      <Footer />
      <div class="mt-5 mx-auto text-center text-sm text-muted-foreground">
        {{ $t('layout.default') }}
      </div>
    </div>
  </main>
</template>
