<script setup lang="ts">
import { availableLocales, loadLanguageAsync } from '~/modules/i18n'

const { locale } = useI18n()
async function toggleLocales() {
  const locales = availableLocales
  const newLocale = locales[(locales.indexOf(locale.value) + 1) % locales.length]
  await loadLanguageAsync(newLocale)
  locale.value = newLocale
}
</script>

<template>
  <header className="fixed top-0 z-50 flex w-full flex-wrap justify-start py-4 text-sm backdrop-blur-sm">
    <nav className="mx-auto flex w-full max-w-[85rem] items-center px-4 justify-between">
      <div className="flex gap-4">
        <div i="carbon-menu" class="block md:hidden" />
        <RouterLink to="/" class-name="basis-full text-left text-xl font-semibold">
          <span className="font-bold sm:inline-block">🎲
            Zero Plan Vite Vue3 Tailwind Starter</span>
        </RouterLink>
      </div>
      <div className="flex items-center">
        <div class="mr-4 hidden md:block">
          <RouterLink to="/example">
            Example
          </RouterLink>
        </div>
        <Button variant="ghost" size="icon" @click="toggleDark()">
          <div i="carbon-sun dark:carbon-moon" />
        </Button>
        <Button variant="ghost" size="icon" @click="toggleLocales()">
          <div i="carbon-globe" />
        </button>
      </div>
    </nav>
  </header>
</template>

<style scoped lang="css">

</style>
