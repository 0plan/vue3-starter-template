<script setup lang="ts">
import type { DialogContentEmits, DialogContentProps } from 'radix-vue'
import type { HTMLAttributes } from 'vue'
import type { SheetVariants } from '.'
import { X } from 'lucide-vue-next'
import {
  DialogClose,
  DialogContent,

  DialogOverlay,
  DialogPortal,
  useForwardPropsEmits,
} from 'radix-vue'
import { computed } from 'vue'
import { cn } from '~/lib/utils'
import { sheetVariants } from '.'

interface SheetContentProps extends DialogContentProps {
  class?: HTMLAttributes['class']
  side?: SheetVariants['side']
}

defineOptions({
  inheritAttrs: false,
})

const props = defineProps<SheetContentProps>()

const emits = defineEmits<DialogContentEmits>()

const delegatedProps = computed(() => {
  const { class: _, side, ...delegated } = props

  return delegated
})

const forwarded = useForwardPropsEmits(delegatedProps, emits)
</script>

<template>
  <DialogPortal>
    <DialogOverlay
      class="data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 fixed inset-0 z-50 bg-black/80"
    />
    <DialogContent
      :class="cn(sheetVariants({ side }), props.class)"
      v-bind="{ ...forwarded, ...$attrs }"
    >
      <slot />

      <DialogClose
        class="ring-offset-background focus:ring-ring data-[state=open]:bg-secondary absolute right-4 top-4 rounded-sm opacity-70 transition-opacity disabled:pointer-events-none hover:opacity-100 focus:outline-none focus:ring-2 focus:ring-offset-2"
      >
        <X class="text-muted-foreground h-4 w-4" />
      </DialogClose>
    </DialogContent>
  </DialogPortal>
</template>
