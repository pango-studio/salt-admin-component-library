<script lang="ts">
export default {
  name: "SltAdminBadge",
};
</script>

<script setup lang="ts">
import { computed } from "vue";

type variationType = "default" | "success" | "warning" | "failure";

const props = withDefaults(
  defineProps<{
    variation?: variationType;
  }>(),
  {
    variation: "default",
  }
);

const variationClasses = computed(() => ({
  "admin-badge-default bg-gray-200": props.variation === "default",
  "admin-badge-success bg-green-200": props.variation === "success",
  "admin-badge-warning bg-yellow-100": props.variation === "warning",
  "admin-badge-failure bg-red-200": props.variation === "failure",
}));
</script>

<template>
  <span
    class="inline-flex items-center px-2 py-1 cursor-pointer hover:opacity-75 my-1 rounded-md text-sm font-medium leading-5"
    :class="variationClasses"
  >
    <span v-if="$slots.label" class="mr-3 italic text-xs text-gray-600">
      <slot name="label"></slot>:
    </span>

    <span v-if="$slots.text" class="text-xs font-medium text-gray-600">
      <slot name="text"></slot>
    </span>
  </span>
</template>
