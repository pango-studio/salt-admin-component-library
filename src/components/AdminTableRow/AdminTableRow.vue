<script lang="ts">
export default {
  name: "SltAdminTableRow",
};
</script>

<script setup lang="ts">
import { computed } from "vue";

import state from "../../state/adminTableState";

const props = defineProps<{
  hasSelect?: boolean;
  index: number;
  value: number;
}>();

const bgClass = computed(() => ({
  "bg-white": props.index % 2 === 0,
  "bg-gray-50": props.index % 2 !== 0,
}));

const isChecked = computed(() => {
  return state.selectedRows.includes(props.value);
});

const toggleChecked = () => {
  if (!state.selectedRows.includes(props.value)) {
    state.selectedRows.push(props.value);
  } else {
    state.selectedRows.filter((item) => item != props.value);
  }
};
</script>

<template>
  <tr :class="bgClass">
    <td
      v-if="hasSelect"
      class="hover:bg-gray-50 cursor-pointer"
      @click="toggleChecked"
    >
      <div class="flex items-center justify-center">
        <input
          type="checkbox"
          class="border form-checkbox cursor-pointer h-4 w-4 text-primary-700 transition duration-150 ease-in-out"
          :checked="isChecked"
        />
      </div>
    </td>
    <slot />
  </tr>
</template>
