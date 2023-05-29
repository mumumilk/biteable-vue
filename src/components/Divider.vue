<script setup>
  const props = defineProps({
    dashed: {
      type: Boolean,
      default: false,
    },
  });
</script>

<template>
  <hr :class="{ dashed: props.dashed }" />
</template>

<style scoped>
  hr {
    border: 0;
    border-top: 1px solid #eee;
  }

  .dashed {
    border-style: dashed;
  }
</style>
