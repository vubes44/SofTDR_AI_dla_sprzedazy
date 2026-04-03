<template>
  <button
    :class="buttonClass"
    :disabled="disabled || loading"
    @click="handleClick"
    type="button"
  >
    <span v-if="!loading">{{ text }}</span>
    <span v-else class="a-button__loader">Loading...</span>
  </button>
</template>

<script setup lang="ts">
import { computed } from "vue";

interface ButtonProps {
  text: string;
  variant: "account-option" | "submit" | "default";
  disabled?: boolean;
  loading?: boolean;
  size?: "sm" | "md" | "lg";
}

const props = defineProps<ButtonProps>({
  text: {
    type: String,
    required: true,
  },
  variant: {
    type: String as () => ButtonProps["variant"],
    default: "default",
  },
  disabled: {
    type: Boolean,
    default: false,
  },
  loading: {
    type: Boolean,
    default: false,
  },
  size: {
    type: String as () => ButtonProps["size"],
    default: "md",
  },
});

const emit = defineEmits<{
  (e: "click"): void;
}>();

const variantClass = computed(() => {
  const map = {
    "account-option": "a-button--account-option",
    submit: "a-button--submit",
    default: "a-button--default",
  };
  return map[props.variant] ?? map.default;
});

const sizeClass = computed(() => {
  const map = {
    sm: "a-button--sm",
    md: "a-button--md",
    lg: "a-button--lg",
  };
  return map[props.size] ?? map.md;
});

const buttonClass = computed(() => [
  "a-button",
  variantClass.value,
  sizeClass.value,
  { "a-button--disabled": props.disabled || props.loading },
]);

function handleClick(event: MouseEvent) {
  if (props.disabled || props.loading) return;
  emit("click");
}
</script>

<style scoped>
.a-button {
  border: 2px solid transparent;
  border-radius: 999px;
  padding: 0.6rem 1.2rem;
  cursor: pointer;
  transition: all 0.2s ease;
  font-weight: 700;
  text-transform: uppercase;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 140px;
}

.a-button--default {
  background: #e2e8f0;
  color: #1f2937;
}

.a-button--default:hover:not(.a-button--disabled) {
  background: #cbd5e1;
}

.a-button--account-option {
  background: transparent;
  border-color: #1d4ed8;
  color: #1d4ed8;
}

.a-button--account-option:hover:not(.a-button--disabled) {
  background: rgba(30, 64, 175, 0.1);
}

.a-button--submit {
  background: #1d4ed8;
  color: #fff;
}

.a-button--submit:hover:not(.a-button--disabled) {
  background: #1e40af;
}

.a-button--disabled {
  opacity: 0.55;
  pointer-events: none;
  cursor: not-allowed;
}

.a-button--sm {
  font-size: 0.75rem;
  padding: 0.45rem 0.9rem;
}

.a-button--md {
  font-size: 0.85rem;
  padding: 0.6rem 1.2rem;
}

.a-button--lg {
  font-size: 1rem;
  padding: 0.75rem 1.5rem;
}

.a-button__loader {
  display: inline-block;
}
</style>
