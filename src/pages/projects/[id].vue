<script setup lang="ts">
import {
  ArrowLeft,
  Calendar,
  CheckCircle2,
  LayoutDashboard,
  Users,
} from 'lucide-vue-next'
import { Avatar, AvatarFallback, AvatarImage } from '~/components/ui/avatar'
import { Badge } from '~/components/ui/badge'
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '~/components/ui/card'
import { Progress } from '~/components/ui/progress'

const route = useRoute()
const projectId = computed(() => route.params.id as string)
const { t, locale } = useI18n()

// Mock data based on ID
const project = computed(() => ({
  id: projectId.value,
  name: locale.value === 'ko'
    ? `프로젝트 ${projectId.value.charAt(0).toUpperCase() + projectId.value.slice(1)}`
    : `Project ${projectId.value.charAt(0).toUpperCase() + projectId.value.slice(1)}`,
  description: locale.value === 'ko'
    ? '핵심 인프라를 현대화하고 shadcn-vue 컴포넌트를 도입하는 작업입니다.'
    : 'Modernizing the core infrastructure and implementing shadcn-vue components.',
  progress: 75,
  status: 'In Progress',
  deadline: '2026-06-30',
  team: [
    { name: 'Alex', avatar: 'https://github.com/antfu.png' },
    { name: 'Sarah', avatar: 'https://github.com/shadcn.png' },
    { name: 'Mike', avatar: 'https://github.com/vuejs.png' },
  ],
  tasks: [
    {
      id: 1,
      title: locale.value === 'ko' ? 'UI 시스템 설정' : 'UI System Setup',
      status: 'Completed',
    },
    {
      id: 2,
      title: locale.value === 'ko' ? 'API 연동' : 'API Integration',
      status: 'In Progress',
    },
    {
      id: 3,
      title: locale.value === 'ko' ? '사용자 테스트' : 'User Testing',
      status: 'Pending',
    },
  ],
}))

const statusLabelMap = {
  'Completed': 'project.completed',
  'In Progress': 'project.in_progress',
  'Pending': 'project.pending',
} as const

function getStatusLabel(status: keyof typeof statusLabelMap | string) {
  return t(statusLabelMap[status as keyof typeof statusLabelMap] ?? status)
}
</script>

<template>
  <div class="max-w-5xl mx-auto space-y-8 animate-fade-in-up text-foreground">
    <!-- Header -->
    <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
      <div class="flex items-center gap-4">
        <Button variant="ghost" size="icon" @click="$router.back()">
          <ArrowLeft class="w-5 h-5" />
        </Button>
        <div>
          <h1 class="text-3xl font-bold flex items-center gap-2">
            <LayoutDashboard class="text-teal-600 dark:text-teal-400" />
            {{ project.name }}
          </h1>
          <p class="text-muted-foreground max-w-2xl">
            {{ project.description }}
          </p>
        </div>
      </div>
      <Badge variant="secondary" class="w-fit text-sm px-3 py-1">
        {{ getStatusLabel(project.status) }}
      </Badge>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
      <!-- Stats Cards -->
      <Card class="border-border bg-card shadow-sm">
        <CardHeader class="pb-2">
          <CardDescription class="flex items-center gap-2">
            <CheckCircle2 class="w-4 h-4 text-green-500" />
            {{ t('project.progress') }}
          </CardDescription>
          <CardTitle class="text-2xl">
            {{ project.progress }}%
          </CardTitle>
        </CardHeader>
        <CardContent>
          <Progress :model-value="project.progress" class="h-2" />
        </CardContent>
      </Card>

      <Card class="border-border bg-card shadow-sm">
        <CardHeader class="pb-2">
          <CardDescription class="flex items-center gap-2">
            <Calendar class="w-4 h-4 text-blue-500" />
            {{ t('project.deadline') }}
          </CardDescription>
          <CardTitle class="text-2xl">
            {{ project.deadline }}
          </CardTitle>
        </CardHeader>
        <CardContent>
          <span class="text-xs text-muted-foreground">{{ t('project.approx_left') }}</span>
        </CardContent>
      </Card>

      <Card class="border-border bg-card shadow-sm">
        <CardHeader class="pb-2">
          <CardDescription class="flex items-center gap-2">
            <Users class="w-4 h-4 text-purple-500" />
            {{ t('project.team_members') }}
          </CardDescription>
          <CardTitle class="flex -space-x-2 overflow-hidden py-1">
            <Avatar v-for="member in project.team" :key="member.name" class="border-2 border-background w-8 h-8">
              <AvatarImage :src="member.avatar" />
              <AvatarFallback>{{ member.name[0] }}</AvatarFallback>
            </Avatar>
          </CardTitle>
        </CardHeader>
        <CardContent>
          <span class="text-xs text-muted-foreground">{{ t('project.active_collaborators', { count: project.team.length }) }}</span>
        </CardContent>
      </Card>
    </div>

    <!-- Tasks List -->
    <Card class="border-border bg-card shadow-sm">
      <CardHeader>
        <CardTitle>{{ t('project.recent_tasks') }}</CardTitle>
      </CardHeader>
      <CardContent class="space-y-4">
        <div v-for="task in project.tasks" :key="task.id" class="flex items-center justify-between p-3 border border-border rounded-lg hover:bg-accent/50 transition-colors bg-background/50">
          <div class="flex items-center gap-3">
            <div
              class="w-2 h-2 rounded-full" :class="[
                task.status === 'Completed' ? 'bg-green-500' : task.status === 'In Progress' ? 'bg-blue-500' : 'bg-muted-foreground',
              ]"
            />
            <span class="font-medium">{{ task.title }}</span>
          </div>
          <Badge :variant="task.status === 'Completed' ? 'default' : 'outline'">
            {{ getStatusLabel(task.status) }}
          </Badge>
        </div>
      </CardContent>
    </Card>
  </div>
</template>
