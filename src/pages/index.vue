<script setup lang="ts">
import { Brush, Github, Laptop, LayoutDashboard, Tent, Users, Zap } from 'lucide-vue-next'
import { Button } from '~/components/ui/button'
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '~/components/ui/card'
import { Input } from '~/components/ui/input'

defineOptions({
  name: 'IndexPage',
})
const user = useUserStore()
const name = ref(user.savedName)

const router = useRouter()
function go() {
  if (name.value)
    router.push(`/users/${encodeURIComponent(name.value)}`)
}

const { t } = useI18n()
</script>

<template>
  <div class="relative flex flex-col items-center justify-center min-h-[60vh] gap-12 text-center text-foreground">
    <!-- Hero Section -->
    <div class="animate-fade-in-up">
      <div class="mb-4 inline-block hover:animate-bounce-alt">
        <Tent class="w-16 h-16 md:w-24 md:h-24 text-teal-600 dark:text-teal-400" />
      </div>
      <h1 class="text-4xl md:text-6xl font-bold mb-4 bg-clip-text text-transparent bg-gradient-to-r from-teal-600 to-indigo-600 dark:from-teal-400 dark:to-indigo-400">
        VueForge
      </h1>
      <p class="text-lg md:text-xl text-muted-foreground max-w-2xl mx-auto">
        {{ t('intro.desc') }}
      </p>
      <p class="mt-2 text-sm text-muted-foreground">
        {{ t('home.subtitle') }}
      </p>
    </div>

    <!-- Interaction Section -->
    <Card class="w-full max-w-md animate-fade-in-up [animation-delay:200ms] backdrop-blur-sm bg-card/80 border-border shadow-sm">
      <CardHeader>
        <CardTitle class="text-left text-base">
          {{ t('intro.whats-your-name') }}
        </CardTitle>
      </CardHeader>
      <CardContent class="flex flex-col gap-4">
        <div class="flex gap-2">
          <Input
            id="input"
            v-model="name"
            :placeholder="t('intro.whats-your-name')"
            type="text"
            autocomplete="false"
            class="flex-grow"
            @keydown.enter="go"
          />
          <Button
            :disabled="!name"
            @click="go"
          >
            {{ t('button.go') }}
          </Button>
        </div>
        <p class="text-xs text-left text-muted-foreground italic">
          {{ t('home.sections.press_enter') }}
        </p>
      </CardContent>
    </Card>

    <!-- Features Grid -->
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 w-full max-w-4xl animate-fade-in-up [animation-delay:400ms]">
      <a href="https://www.shadcn-vue.com/" target="_blank" class="group">
        <Card class="h-full border-border bg-card hover:scale-105 transition-transform shadow-sm">
          <CardHeader>
            <Brush class="w-10 h-10 mb-2 text-purple-500 group-hover:text-purple-400 transition-colors" />
            <CardTitle>{{ t('home.feature.shadcn_title') }}</CardTitle>
            <CardDescription>{{ t('home.feature.shadcn_desc') }}</CardDescription>
          </CardHeader>
        </Card>
      </a>
      <a href="https://github.com/vuejs/core" target="_blank" class="group">
        <Card class="h-full border-border bg-card hover:scale-105 transition-transform shadow-sm">
          <CardHeader>
            <Laptop class="w-10 h-10 mb-2 text-green-500 group-hover:text-green-400 transition-colors" />
            <CardTitle>{{ t('home.feature.vue_title') }}</CardTitle>
            <CardDescription>{{ t('home.feature.vue_desc') }}</CardDescription>
          </CardHeader>
        </Card>
      </a>
      <a href="https://vitejs.dev" target="_blank" class="group">
        <Card class="h-full border-border bg-card hover:scale-105 transition-transform shadow-sm">
          <CardHeader>
            <Zap class="w-10 h-10 mb-2 text-yellow-500 group-hover:text-yellow-400 transition-colors" />
            <CardTitle>{{ t('home.feature.vite_title') }}</CardTitle>
            <CardDescription>{{ t('home.feature.vite_desc') }}</CardDescription>
          </CardHeader>
        </Card>
      </a>
    </div>

    <!-- Dynamic Demos Section -->
    <div class="w-full max-w-4xl space-y-6 animate-fade-in-up [animation-delay:600ms]">
      <h2 class="text-2xl font-bold text-left px-2 text-foreground">
        {{ t('home.sections.demos') }}
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
        <RouterLink to="/projects/vueforge-dashboard">
          <Card class="hover:bg-accent/50 transition-colors cursor-pointer group border-border bg-card shadow-sm">
            <CardHeader class="flex flex-row items-center gap-4 space-y-0">
              <div class="p-2 bg-teal-100 dark:bg-teal-900/30 rounded-lg group-hover:scale-110 transition-transform">
                <LayoutDashboard class="w-6 h-6 text-teal-600" />
              </div>
              <div class="text-left">
                <CardTitle class="text-lg">
                  {{ t('home.sections.project') }}
                </CardTitle>
                <CardDescription>{{ t('home.sections.project_path') }}</CardDescription>
              </div>
            </CardHeader>
          </Card>
        </RouterLink>

        <RouterLink to="/users/0plan">
          <Card class="hover:bg-accent/50 transition-colors cursor-pointer group border-border bg-card shadow-sm">
            <CardHeader class="flex flex-row items-center gap-4 space-y-0">
              <div class="p-2 bg-indigo-100 dark:bg-indigo-900/30 rounded-lg group-hover:scale-110 transition-transform">
                <Users class="w-6 h-6 text-indigo-600" />
              </div>
              <div class="text-left">
                <CardTitle class="text-lg">
                  {{ t('home.sections.profile') }}
                </CardTitle>
                <CardDescription>{{ t('home.sections.profile_path') }}</CardDescription>
              </div>
            </CardHeader>
          </Card>
        </RouterLink>
      </div>
    </div>

    <div class="mt-8">
      <Button variant="outline" as-child>
        <a
          rel="noreferrer"
          href="https://github.com/0plan/vue3-starter-template"
          target="_blank"
          class="flex items-center gap-2"
        >
          <Github class="w-4 h-4" />
          {{ t('home.sections.github') }}
        </a>
      </Button>
    </div>
  </div>
</template>

<route lang="yaml">
meta:
  layout: default
</route>
