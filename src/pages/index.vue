<script setup lang="ts">
defineOptions({
  name: 'IndexPage',
})
const user = useUserStore()
const name = ref(user.savedName)

const router = useRouter()
function go() {
  if (name.value)
    router.push(`/hi/${encodeURIComponent(name.value)}`)
}

const { t } = useI18n()
</script>

<template>
  <div class="flex flex-col items-center">
    <div text-4xl>
      <div i-carbon-campsite inline-block />
    </div>
    <p>
      <a rel="noreferrer" href="https://github.com/antfu/vitesse" target="_blank">
        Vitesse
      </a>
    </p>
    <p>
      <em text-sm opacity-75>{{ t('intro.desc') }}</em>
    </p>

    <div class="max-w-sm flex">
      <Input
        v-model="name"
        :placeholder="t('intro.whats-your-name')"
        @keydown.enter="go"
      />
      <Button :disabled="!name" size="sm" variant="default" @click="go">
        {{ t('button.go') }}
      </Button>
    </div>
  </div>
</template>

<route lang="yaml">
meta:
  layout: default
</route>
