<script setup lang="ts">
import {
  ContextMenuItem,
  type ContextMenuItemEmits,
  type ContextMenuItemProps,
  useEmitAsProps,
} from 'radix-vue'

const props = defineProps<ContextMenuItemProps & { class?: string, inset?: boolean }>()
const emits = defineEmits<ContextMenuItemEmits>()
</script>

<template>
  <ContextMenuItem
    v-bind="{ ...props, ...useEmitAsProps(emits) }"
    class="relative flex cursor-default select-none text-12px items-center rounded-7px px-2 py-1.5 outline-none focus:bg-[#5021ff] focus:text-white data-[disabled]:pointer-events-none data-[disabled]:opacity-50"

    :class="props.class && (inset && 'pl-8')"
  >
    <slot />
  </ContextMenuItem>
</template>
