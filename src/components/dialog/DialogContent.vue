<script setup lang="ts">
import {
  DialogContent,
  type DialogContentEmits,
  type DialogContentProps,
  DialogOverlay,
  DialogPortal,
  useEmitAsProps,
} from 'radix-vue'

const props = defineProps<DialogContentProps & { class?: string }>()
const emits = defineEmits<DialogContentEmits>()

const emitsAsProps = useEmitAsProps(emits)
</script>

<template>
  <DialogPortal>
    <DialogOverlay
      class="
        fixed inset-0 z-50
        bg-background/80
        bg-[#00000034]
        backdrop-blur-5px

      "
    />
    <Teleport to="body">
      <DialogContent
        class="
          fixed left-[50%] top-[50%] z-50
          grid w-full max-w-lg
          translate-x-[-50%] translate-y-[-50%]
          gap-4
          bg-[#252836] text-white
          p-6 shadow-lg rounded-20px

          data-[state=open]:animate-[dialog-in_0.3s]
          data-[state=closed]:animate-[dialog-out_0.3s]
        "
        :class="props.class"
        v-bind="{ ...props, ...emitsAsProps }"
      >
        <slot />

        <!-- <DialogClose
          class="absolute top-3 right-3 p-0.5 transition-colors rounded-md hover:bg-secondary"
        >
          <svg class="w-4 h-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18 6L6 18M6 6l12 12" /></svg>
          <span class="sr-only">Close</span>
        </DialogClose> -->
      </DialogContent>
    </Teleport>
  </DialogPortal>
</template>
