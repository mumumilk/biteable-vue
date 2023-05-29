<template>
  <div @keyup.esc="hide">
    <slot name="trigger">
      <Button ref="trigger" class="trigger" @click="toggle">trigger</Button>
    </slot>
    <Teleport to="body">
      <div class="modal-overlay">
        <div ref="modal" v-on-click-outside="clickedOutside" class="modal">
          <button class="close" @click="hide">
            <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24">
              <path
                fill="none"
                stroke="currentColor"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="m21 21l-9-9m0 0L3 3m9 9l9-9m-9 9l-9 9"
              />
            </svg>
          </button>
          <slot :hide="hide"></slot>
        </div>
      </div>
    </Teleport>
  </div>
</template>

<script setup>
  import { ref } from 'vue';
  import Button from './Button.vue';
  import { vOnClickOutside } from '@vueuse/components';
  import { useFocusTrap } from '@vueuse/integrations/useFocusTrap';

  const trigger = ref();
  const modal = ref();

  const { activate: trapFocus, deactivate: releaseFocus } = useFocusTrap(modal);

  const clickedOutside = [
    (ev) => {
      hide();
    },
    { ignore: [trigger] },
  ];

  function show() {
    document.body.setAttribute('overlay', '');
    trapFocus();
  }

  function hide() {
    document.body.removeAttribute('overlay');
    releaseFocus();
  }

  function toggle() {
    if (document.body.hasAttribute('overlay')) {
      hide();
    } else {
      show();
    }
  }
</script>

<style scoped>
  .modal-overlay {
    position: fixed;
    top: 0;
    width: 100%;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 1;
    visibility: hidden;
    opacity: 0;
    transition: opacity 0.3s ease-in-out;
    display: grid;
    place-items: center;
  }

  :global(body[overlay] .modal-overlay) {
    visibility: visible;
    opacity: 1;
  }

  :global(body[overlay] #app) {
    margin-right: 15px;
  }

  :global(body[overlay]) {
    overflow: hidden;
  }

  .modal-container {
    width: 100%;
    height: 100vh;
    z-index: 1;
    display: none;
    place-items: center;
  }

  @keyframes appear {
    from {
      transform: translateY(-300%);
    }

    to {
      transform: translateY(0);
    }
  }

  .modal {
    background: white;
    width: 100%;
    max-width: 40rem;
    border-radius: 1rem;
    padding: 3rem 1.5rem 1.5rem;
    box-shadow: 0 0 6rem 0 rgba(0, 0, 0, 0.3);
    animation: appear 0.5s;
    position: relative;
  }

  .close {
    position: absolute;
    padding: 0.75rem;
    border: none;
    top: 0.5rem;
    right: 0.5rem;
    cursor: pointer;
    color: #161824;
    background: transparent;
    display: grid;
    place-items: center;
    transition: color 0.1s ease;
  }

  .close:hover {
    color: var(--color-primary);
  }

  .close:focus {
    outline-color: var(--color-primary);
    color: var(--color-primary);
  }
</style>
