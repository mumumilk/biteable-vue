<template>
  <li>
    <a
      role="menuitem"
      tabindex="0"
      v-bind="attrs"
      @click="interceptAsClick"
      target="_blank"
      @keyup.enter="interceptAsClick"
    >
      <slot></slot>
    </a>
  </li>
</template>

<script setup>
  import { inject, useAttrs } from 'vue';
  import { MenuSymbol } from '../symbols';

  const { hide: hideMenu } = inject(MenuSymbol);

  const attrs = useAttrs();
  const emit = defineEmits(['click']);

  function interceptAsClick(e) {
    hideMenu();
    emit('click', e);
  }
</script>

<script>
  export default {
    inheritAttrs: false,
  };
</script>

<style scoped>
  li {
    overflow: hidden;
  }

  a {
    display: block;
    width: 100%;
    box-sizing: border-box;
    user-select: none;
    transition: background-color 1s ease;
    border: none;
    padding: 0.5rem 1rem;
    background-color: transparent;
    outline: none;
    font-size: 1rem;
    font-weight: 300;
    font-family: inherit;
    margin: 0;
    cursor: pointer;
    text-align: left;
  }

  a:hover,
  a:focus {
    background-color: var(--color-hover);
    outline: none;
    border: none;
  }
</style>
