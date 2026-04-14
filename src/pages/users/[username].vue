<script setup lang="ts">
import {
  ArrowLeft,
  Github,
  Link as LinkIcon,
  MapPin,
  MessageSquare,
  Twitter,
  UserPlus,
} from 'lucide-vue-next'
import { Avatar, AvatarFallback, AvatarImage } from '~/components/ui/avatar'
import { Button } from '~/components/ui/button'
import { Card, CardContent, CardHeader } from '~/components/ui/card'

const GITHUB_USERNAME_SANITIZE_RE = /[^a-z0-9]/gi

const route = useRoute()
const username = computed(() => route.params.username as string)
const { t, locale } = useI18n()

// Mock data based on username
const profile = computed(() => ({
  username: username.value,
  fullName: username.value.split('-').map(s => s.charAt(0).toUpperCase() + s.slice(1)).join(' '),
  avatar: `https://github.com/${username.value.replace(GITHUB_USERNAME_SANITIZE_RE, '')}.png`,
  bio: t('user.bio'),
  location: locale.value === 'ko' ? '서울, 대한민국' : 'Seoul, Korea',
  website: 'https://0plan.dev',
}))
</script>

<template>
  <div class="max-w-3xl mx-auto animate-fade-in-up">
    <Button variant="ghost" class="mb-6" @click="$router.back()">
      <ArrowLeft class="w-4 h-4 mr-2" />
      {{ t('button.back') }}
    </Button>

    <Card class="overflow-hidden border-none shadow-xl bg-gradient-to-b from-teal-500/10 to-background">
      <div class="h-32 bg-gradient-to-r from-teal-600 to-indigo-600" />
      <CardHeader class="relative pb-0">
        <div class="absolute -top-16 left-6">
          <Avatar class="w-32 h-32 border-4 border-background shadow-lg">
            <AvatarImage :src="profile.avatar" />
            <AvatarFallback class="text-2xl">
              {{ profile.username[0].toUpperCase() }}
            </AvatarFallback>
          </Avatar>
        </div>
        <div class="mt-16 flex flex-col md:flex-row md:items-center justify-between gap-4 py-4">
          <div>
            <h1 class="text-3xl font-bold">
              {{ profile.fullName }}
            </h1>
            <p class="text-teal-600 dark:text-teal-400 font-medium">
              @{{ profile.username }}
            </p>
          </div>
          <div class="flex gap-2">
            <Button class="rounded-full px-6">
              <UserPlus class="w-4 h-4 mr-2" />
              {{ t('user.follow') }}
            </Button>
            <Button variant="outline" size="icon" class="rounded-full" :title="t('user.message')">
              <MessageSquare class="w-4 h-4" />
            </Button>
          </div>
        </div>
      </CardHeader>

      <CardContent class="space-y-6 pb-10">
        <p class="text-lg leading-relaxed max-w-2xl">
          {{ profile.bio }}
        </p>

        <div class="flex flex-wrap gap-4 text-sm text-muted-foreground">
          <div class="flex items-center gap-1">
            <MapPin class="w-4 h-4" />
            {{ t('user.location') }}: {{ profile.location }}
          </div>
          <div class="flex items-center gap-1 hover:text-foreground cursor-pointer transition-colors">
            <LinkIcon class="w-4 h-4" />
            {{ t('user.website') }}: {{ profile.website }}
          </div>
        </div>

        <div class="flex gap-4 pt-2">
          <Button variant="ghost" size="icon" class="text-muted-foreground hover:text-blue-400">
            <Twitter class="w-5 h-5" />
          </Button>
          <Button variant="ghost" size="icon" class="text-muted-foreground hover:text-foreground">
            <Github class="w-5 h-5" />
          </Button>
        </div>
      </CardContent>
    </Card>
  </div>
</template>
