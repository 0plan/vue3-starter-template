<script setup lang="ts">
import { Github, Languages, Moon, Sun } from 'lucide-vue-next'
import { availableLocales, loadLanguageAsync } from '~/modules/i18n'

const { locale, t } = useI18n()

async function toggleLocales() {
  const locales = availableLocales
  const newLocale = locales[(locales.indexOf(locale.value) + 1) % locales.length]
  await loadLanguageAsync(newLocale)
  locale.value = newLocale
}
</script>

<template>
  <nav class="text-xl mt-6 flex justify-center items-center gap-4">
    <Button variant="ghost" size="icon" :title="t('button.toggle_dark')" @click="toggleDark()">
      <Sun class="w-5 h-5 rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0" />
      <Moon class="absolute w-5 h-5 rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100" />
    </Button>

    <Button variant="ghost" size="icon" as-child>
      <a rel="noreferrer" href="https://github.com/0plan/vue3-starter-template" target="_blank" :title="t('home.sections.github')">
        <Github class="w-5 h-5" />
      </a>
    </Button>

    <Button variant="ghost" size="icon" :title="t('button.toggle_langs')" @click="toggleLocales()">
      <Languages class="w-5 h-5" />
    </Button>
  </nav>
</template>
