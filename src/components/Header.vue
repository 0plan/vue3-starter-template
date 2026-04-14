<script setup lang="ts">
import { Github, Languages, Menu, Moon, Sun, Tent } from 'lucide-vue-next'
import { availableLocales, loadLanguageAsync } from '~/modules/i18n'

const { locale, t } = useI18n()

async function toggleLocales() {
  const locales = availableLocales
  const newLocale = locales[(locales.indexOf(locale.value) + 1) % locales.length]
  await loadLanguageAsync(newLocale)
  locale.value = newLocale
}

const showMobileMenu = ref(false)
</script>

<template>
  <header
    class="fixed top-0 w-full z-50 transition-all duration-300 border-b border-border backdrop-blur-md bg-background/80"
  >
    <nav class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
      <div class="flex items-center gap-4">
        <RouterLink to="/" class="flex items-center gap-2 group">
          <Tent class="w-6 h-6 text-teal-600 dark:text-teal-400 group-hover:scale-110 transition-transform" />
          <span class="text-xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-teal-600 to-indigo-600 dark:from-teal-400 dark:to-indigo-400">
            VueForge
          </span>
        </RouterLink>
      </div>

      <div class="hidden md:flex items-center gap-2">
        <Button variant="ghost" as-child>
          <RouterLink to="/about">
            {{ t('button.about') || 'About' }}
          </RouterLink>
        </Button>
        <Button variant="ghost" size="icon" as-child>
          <a href="https://github.com/0plan/vue3-starter-template" target="_blank" rel="noreferrer" :title="t('home.sections.github')">
            <Github class="w-5 h-5" />
          </a>
        </Button>

        <div class="h-6 w-px bg-border mx-2" />

        <Button variant="ghost" size="icon" class="relative" :title="t('button.toggle_dark')" @click="toggleDark()">
          <Sun class="w-5 h-5 rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0" />
          <Moon class="absolute w-5 h-5 rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100" />
        </Button>
        <Button variant="ghost" size="icon" :title="t('button.toggle_langs')" @click="toggleLocales()">
          <Languages class="w-5 h-5" />
        </Button>
      </div>

      <!-- Mobile Menu Button -->
      <Button variant="ghost" size="icon" class="md:hidden" @click="showMobileMenu = !showMobileMenu">
        <Menu class="w-6 h-6" />
      </Button>
    </nav>
  </header>
</template>
