<template>
  <div @keyup.esc="hide">
    <slot name="trigger">
      <Button aria-haspopup="true" ref="trigger" class="trigger" @click="toggle">trigger</Button>
    </slot>
    <div ref="menu" role="menu" v-on-click-outside="clickedOutside" class="menu">
      <ul>
        <slot :hide="hide"></slot>
      </ul>
      <div id="arrow" data-popper-arrow></div>
    </div>
  </div>
</template>

<script setup>
  import { onMounted, provide, ref } from 'vue';
  import Button from './Button.vue';
  import { createPopper } from '@popperjs/core';
  import { vOnClickOutside } from '@vueuse/components';
  import { useFocusTrap } from '@vueuse/integrations/useFocusTrap';
  import { MenuSymbol } from '../symbols';

  const trigger = ref();
  const menu = ref();

  const { activate: trapFocus, deactivate: releaseFocus } = useFocusTrap(menu);

  const props = defineProps({
    placement: {
      type: String,
      default: 'bottom-start',
    },
  });

  function show() {
    menu.value.setAttribute('data-show', '');
    trapFocus();
  }

  function hide() {
    menu.value.removeAttribute('data-show');
    releaseFocus();
  }

  function toggle() {
    if (menu.value.hasAttribute('data-show')) {
      hide();
    } else {
      show();
    }
  }

  const clickedOutside = [
    (ev) => {
      hide();
    },
    { ignore: [trigger] },
  ];

  onMounted(() => {
    createPopper(trigger.value.component, menu.value, {
      placement: props.placement,
      modifiers: [
        {
          name: 'offset',
          options: {
            offset: [0, 8],
          },
        },
      ],
    });
  });

  provide(MenuSymbol, {
    hide,
  });
</script>

<style scoped>
  @keyframes open {
    from {
      opacity: 0;
    }

    to {
      opacity: 1;
    }
  }

  .menu {
    background-color: white;
    visibility: hidden;
    border-radius: 0.25rem;
    box-shadow: rgba(0, 0, 0, 0.17) 0 2px 1rem, rgba(0, 0, 0, 0.2) 0 0 1px;
    font-weight: 300;
    z-index: 2;
    padding: 0.5rem 0;
    display: flex;
    flex-direction: column;
  }

  #arrow {
    width: 8px;
    height: 8px;
    position: absolute;
    background: transparent;
  }

  #arrow:before {
    content: '';
    width: 8px;
    height: 8px;
    position: absolute;
    transform: rotate(45deg);
    background: white;
  }

  .menu[data-popper-placement^='top'] > #arrow {
    bottom: -4px;
  }

  .menu[data-popper-placement^='bottom'] > #arrow {
    top: -4px;
  }

  .menu[data-popper-placement^='left'] > #arrow {
    right: -4px;
  }

  .menu[data-popper-placement^='right'] > #arrow {
    left: -4px;
  }

  .menu[data-show] {
    visibility: visible;
    animation: open 0.5s ease;
  }
</style>
