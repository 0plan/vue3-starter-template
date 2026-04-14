<script setup lang="ts">
import { computed } from 'vue'
import { useI18n } from 'vue-i18n'
import AboutEn from '../locales/pages/about/en.md'
import AboutKo from '../locales/pages/about/ko.md'

const { locale } = useI18n()

const AboutContent = computed(() => {
  return locale.value === 'ko' ? AboutKo : AboutEn
})
</script>

<template>
  <div class="animate-fade-in-up">
    <component :is="AboutContent" :key="locale" />

    <div class="mt-10 pt-6 border-t border-border text-center">
      <Button variant="outline" @click="$router.back()">
        {{ $t('button.back') }}
      </Button>
    </div>
  </div>
</template>

<route lang="yaml">
meta:
  layout: default
</route>
