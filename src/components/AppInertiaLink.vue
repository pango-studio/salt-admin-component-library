<template>
  <Link v-bind="props" @click="$emit('click')" :as="inertiaAs">
    <slot></slot>
  </Link>
</template>

<script setup lang="ts">
import { computed } from "vue";

const props = withDefaults(
  defineProps<{
    data?: Record<string, unknown>;
    headers?: Record<string, unknown>;
    href: string;
    method?: string;
    only?: string[];
    preserveScroll?: boolean;
    preserveState?: boolean;
    replace?: boolean;
  }>(),
  { headers: () => ({}), method: "get", only: () => [] }
);

const inertiaAs = computed(() => {
  return props.method.toLowerCase() !== "get" ? "button" : "a";
});
</script>
