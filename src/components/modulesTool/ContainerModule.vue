<template>
  <div class="mx-5" :class="double ? 'flex-grow-4' : 'flex-grow-1'">
    <h3 class="mb-1">{{ title }}</h3>
    <div class="container-module">
      <v-btn
        class="iconClose"
        variant="text"
        icon="mdi-minus-circle"
        color="#D34949"
        @click="updateSelectedModules(props.id)"
      ></v-btn>
      <v-sheet :elevation="4" rounded="lg" class="pa-4">
        <slot></slot>
      </v-sheet>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  title: String,
  double: Boolean,
  id: Number,
  selectedModules: Object,
});

const emit = defineEmits(['updateSelectedModules'])

const updateSelectedModules = (idToRemove) => {
  const updatedData = props.selectedModules.filter(item => item.id !== idToRemove);
  emit('updateSelectedModules', updatedData)
}
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
