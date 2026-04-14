<script lang="ts">
import type { HTMLAttributes, InjectionKey } from 'vue'
import { useId } from 'radix-vue'
import { provide } from 'vue'
import { cn } from '~/lib/utils'

export const FORM_ITEM_INJECTION_KEY
  = Symbol('FormItem') as InjectionKey<string>
</script>

<script lang="ts" setup>
const props = defineProps<{
  class?: HTMLAttributes['class']
}>()

const id = useId()
provide(FORM_ITEM_INJECTION_KEY, id)
</script>

<template>
  <div :class="cn('space-y-2', props.class)">
    <slot />
  </div>
</template>
