<template>
  <div class="m-label-and-input" :class="layout">
    <ALabel :type="'input-label'" :margin="labelMargin">{{ label }}</ALabel>
    <AInput
      :modelValue="modelValue"
      @update:modelValue="$emit('update:modelValue', $event)"
      :type="inputType"
      :placeholder="inputPlaceholder"
      :disabled="inputDisabled"
    />
  </div>
</template>
<script setup lang="ts">
import ALabel from "../atoms/ALabel.vue";
import AInput from "../atoms/AInput.vue";
withDefaults(
  defineProps<{
    label: string;
    modelValue?: string;
    labelMargin?: string;
    inputType?: "text" | "password";
    inputPlaceholder?: string;
    inputDisabled?: boolean;
    layout?: "vertical" | "horizontal";
  }>(),
  {
    modelValue: "",
    labelType: "input-label",
    labelMargin: "0 0 8px 0",
    inputType: "text",
    inputPlaceholder: "",
    inputDisabled: false,
    layout: "horizontal",
  },
);

defineEmits<{
  "update:modelValue": [value: string];
}>();
</script>
<style scoped lang="scss">
.m-label-and-input {
  display: flex;
  flex-direction: column;
}
.m-label-and-input.horizontal {
  flex-direction: row;
  align-items: center;

  .a-label {
    margin-right: 12px;
    margin-bottom: 0;
  }
}
</style>
