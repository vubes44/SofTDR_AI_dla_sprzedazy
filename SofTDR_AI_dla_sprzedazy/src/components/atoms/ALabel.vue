<template>
  <component
    :is="tag"
    :class="['a-label', typeClass]"
    :style="computedStyle"
  >
    <slot />
  </component>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import type { PropType } from 'vue'

const props = defineProps({
  type: {
    type: String as PropType<'title-label'|'header-label'|'section-label'|'input-label'|'paragraph'|'another'>,
    default: 'paragraph',
  },
  margin: {
    type: String,
    default: '0',
  },
})

const tag = computed(() => {
  if (props.type === 'title-label' || props.type === 'header-label') return 'h1'
  if (props.type === 'section-label') return 'h2'
  if (props.type === 'input-label') return 'label'
  if (props.type === 'paragraph') return 'p'
  if (props.type === 'another') return 'span'
  return 'span'
})

const typeClass = computed(() => {
  if (props.type === 'title-label' || props.type === 'header-label') return 'title-label'
  if (props.type === 'section-label') return 'section-label'
  if (props.type === 'input-label') return 'input-label'
  if (props.type === 'paragraph') return 'paragraph'
  if (props.type === 'another') return 'another'
  return ''
})

const computedStyle = computed(() => ({
  margin: props.margin,
}))
</script>

<style scoped>
.a-label {
  display: inline-block;
}

.title-label {
  font-size: 2rem;
  font-weight: 700;
  line-height: 1.2;
  margin: 0;
}

.section-label {
  font-size: 1.5rem;
  font-weight: 600;
  line-height: 1.3;
  margin: 0;
}

.input-label {
  font-size: 0.9rem;
  font-weight: 500;
  color: #333;
}

.paragraph {
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.6;
  margin: 0;
}

.another {
  font-size: 0.95rem;
  font-weight: 400;
  color: #666;
}
</style>
