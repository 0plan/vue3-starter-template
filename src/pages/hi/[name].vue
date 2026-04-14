<script setup lang="ts">
const router = useRouter()
const route = useRoute()
const user = useUserStore()
const { t } = useI18n()

watchEffect(() => {
  user.setNewName(route.params.name as string)
})
</script>

<template>
  <div class="text-foreground">
    <div class="text-4xl">
      <div class="i-carbon-pedestrian inline-block" />
    </div>
    <p>
      {{ t('intro.hi', { name: user.savedName }) }}
    </p>

    <p class="text-sm text-muted-foreground">
      <em>{{ t('intro.dynamic-route') }}</em>
    </p>

    <template v-if="user.otherNames.length">
      <p class="mt-4 text-sm">
        <span class="text-muted-foreground">{{ t('intro.aka') }}:</span>
        <ul>
          <li v-for="otherName in user.otherNames" :key="otherName">
            <RouterLink :to="`/hi/${otherName}`" replace>
              {{ otherName }}
            </RouterLink>
          </li>
        </ul>
      </p>
    </template>

    <div class="m-3 mt-6">
      <Button
        class="text-sm"
        @click="router.back()"
      >
        {{ t('button.back') }}
      </Button>
    </div>
  </div>
</template>
