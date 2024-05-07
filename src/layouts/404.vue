<script setup lang="ts">
const router = useRouter()
const { t } = useI18n()
</script>

<template>
  <main class="px-4 py-10" text="center">
    <div class="text-4xl">
      <div i-carbon-warning inline-block />
    </div>
    <RouterView />
    <div class="py-4">
      <Button size="sm" @click="router.back()">
        {{ t('button.back') }}
      </Button>
    </div>
  </main>
</template>
