<script setup>
  import { computed, ref } from 'vue';
  import Spinner from './Spinner.vue';

  const comp = ref();

  const props = defineProps({
    variant: {
      type: String,
      default: 'default',
      validator: (value) => {
        return ['default', 'primary', 'secondary', 'warning', 'danger', 'muted'].includes(value);
      },
    },
    size: {
      type: String,
      default: 'regular',
      validator: (value) => {
        return ['small', 'regular', 'large'].includes(value);
      },
    },
    loading: {
      type: Boolean,
      default: false,
    },
    href: {
      type: [String, null],
      default: null,
    },
  });

  const tag = computed(() => (props.href ? 'a' : 'button'));

  defineExpose({ component: comp });
</script>

<template>
  <component
    ref="comp"
    :is="tag"
    :href="props.href"
    target="_blank"
    class="base"
    :class="[props.size, props.variant, { loading: props.loading }]"
  >
    <Spinner v-show="props.loading" class="spinner" :class="[props.variant]" />
    <slot></slot>
  </component>
</template>

<style scoped>
  /* BASE */
  .base {
    font-family: Brown;
    font-weight: var(--font-bold);
    border-radius: var(--border-radius);
    border: 0;
    cursor: pointer;
    font-size: 1rem;
    position: relative;
    display: inline-block;
    text-decoration: none;
    text-align: center;
  }

  .base:focus,
  .base:hover {
    outline: 0;
    box-shadow: 0 0 0 0 var(--color-white), 0 0 0 var(--border-radius) var(--color-primary);
  }

  .base:disabled {
    opacity: 0.5;
    cursor: not-allowed;
    color: var(--color-gray-600);
    background-color: var(--color-white);
    box-shadow: 0 0 0 2px var(--color-gray-600) inset;
    background-image: none;
  }

  /* SIZE */
  .small {
    padding: 0.5em 1.5em;
  }
  .regular {
    padding: 0.75em 1.5em;
  }

  .large {
    padding: 1em 1.7em;
  }

  /* VARIANTS */
  .default {
    color: var(--color-gray-800);
    background-color: var(--color-gray-200);
  }

  .primary {
    background-color: var(--color-primary);
    color: var(--color-primary-dark);
  }

  .secondary {
    color: var(--color-white);
    background: var(--color-secondary);
  }

  .warning {
    color: var(--color-secondary);
    background: var(--color-warning);
  }

  .danger {
    color: var(--color-white);
    background-image: var(--background-danger);
  }

  .muted {
    color: var(--color-primary-dark);
    background-color: inherit;
  }

  /* LOADING */
  .loading {
    color: transparent;
  }

  .spinner {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    width: 1.75em;
    height: 1.75em;
  }
</style>
