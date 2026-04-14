<script setup lang="ts">
// https://github.com/vueuse/head
// you can use this to manipulate the document head in any components,
// they will be rendered correctly in the html results with vite-ssg
const { t } = useI18n()

useHead(() => ({
  title: t('site.title'),
  meta: [
    {
      name: 'description',
      content: t('site.description'),
    },
    {
      name: 'theme-color',
      content: isDark.value ? '#00aba9' : '#ffffff',
    },
  ],
  link: [
    {
      rel: 'icon',
      type: 'image/svg+xml',
      href: () => preferredDark.value ? '/favicon-dark.svg' : '/favicon.svg',
    },
  ],
}))
</script>

<template>
  <div class="relative min-h-screen overflow-x-hidden bg-background text-foreground font-sans">
    <RouterView />
  </div>
</template>
