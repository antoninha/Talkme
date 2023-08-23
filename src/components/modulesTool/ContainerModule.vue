<template>
  <div class="mx-5" :class="double ? 'flex-grow-4' : 'flex-grow-1'">
    <h3 class="mb-1">{{ title }}</h3>
    <div class="container-module">
      <v-btn
        class="iconClose"
        variant="text"
        icon="mdi-minus-circle"
        color="#D34949"
      ></v-btn>
      <v-sheet :elevation="4" rounded="lg" class="pa-4">
        <slot></slot>
      </v-sheet>
    </div>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  double: Boolean,
});
</script>

<style>
.container-module {
  position: relative;
}
.container-module .iconClose {
  position: absolute;
  top: 0;
  right: 0;
  transform: translate(50%, -50%);
}
</style>
