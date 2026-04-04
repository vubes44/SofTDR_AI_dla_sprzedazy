<template>
  <input
    :type="type"
    :placeholder="placeholder"
    :value="modelValue"
    :disabled="disabled"
    :class="['a-input', `a-input--${type}`]"
    @input="$emit('update:modelValue', $event.target.value)"
  />
</template>

<script setup lang="ts">
withDefaults(
  defineProps<{
    type?: "text" | "password";
    placeholder?: string;
    modelValue?: string;
    disabled?: boolean;
  }>(),
  {
    type: "text",
    placeholder: "",
    modelValue: "",
    disabled: false,
  },
);

defineEmits<{
  "update:modelValue": [value: string];
}>();
</script>

<style scoped>
.a-input {
  padding: 10px 14px;
  font-size: 13px;
  font-family: inherit;
  border: 2px solid #e0e0e0;
  border-radius: 6px;
  transition: all 0.3s ease;
  outline: none;
  width: 300px;
  box-sizing: border-box;
  background-color: #fff;
  color: #333;
}

.a-input:hover {
  border-color: #b0b0b0;
}

.a-input:focus {
  border-color: #2563eb;
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
}

.a-input:disabled {
  background-color: #f5f5f5;
  color: #999;
  cursor: not-allowed;
  border-color: #d0d0d0;
}

/* Text input specific styles */
.a-input--text {
  background-image: none;
}

/* Password input specific styles */
.a-input--password {
  letter-spacing: 0.15em;
}

.a-input--password::placeholder {
  letter-spacing: normal;
  font-family: inherit;
}

/* Placeholder styles */
.a-input::placeholder {
  color: #999;
  opacity: 1;
}

/* Browser-specific placeholder styles */
.a-input::-webkit-input-placeholder {
  color: #999;
}

.a-input::-moz-placeholder {
  color: #999;
}

.a-input:-ms-input-placeholder {
  color: #999;
}

.a-input::-ms-input-placeholder {
  color: #999;
}
</style>
