<template>
  <fieldset>
    <legend>Which is the best color? {{ val }}</legend>
    <div>
      <label for="purple">Purple</label>
      <input hidden name="colorOption" type="radio" id="purple" :value="true" v-model="val" />
      <label for="aubergine">Aubergine</label>
      <input hidden name="colorOption" type="radio" id="aubergine" :value="false" v-model="val" />
    </div>
  </fieldset>
</template>

<script setup>
  import { ref } from 'vue';

  const val = ref('');
</script>

<style scoped>
  div {
    display: flex;
    border-radius: 3px;
  }

  label:first-child {
    background-color: red;
  }
</style>
