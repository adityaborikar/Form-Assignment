<template>
  <div>
    <label class="label cursor-pointer">
      <span class="label-text mr-2">{{ label }}</span>
      <input type="checkbox" class="checkbox" :value="value"
        @change="$emit('update:modelValue', $event.target.value)" />
    </label>
  </div>
</template>

<script setup>
defineProps({
  checkBoxFieldName: String,
  value: { type: String, default: undefined },
  label: { type: String, default: "", required: true },
  modelValue: {
    type: [Array, Boolean],
    default: () => [],
  },
})
</script>