<template>
    <div class="drawer v-col-3" :class="{active: props.display}">
      <div class="close">
        <v-btn variant="text" icon="mdi-close" color="#CA8702" @click="$emit('toggle', false)"></v-btn>
      </div>
        <h2 class="mt-5 mb-5">Votre sélection</h2>
        <v-divider class="mb-10"></v-divider>

        <div v-for="(selectedModule, index) in selectedModules" :key="index">
          <ItemResultModule @updateSelectedModules="updateSelectedModules" :selectedModule="selectedModule" :selectedModules="selectedModules" />
        </div>

    </div>
</template>

<script setup>
import ItemResultModule from './ItemResultModule.vue';
import { defineProps } from 'vue';

const emit = defineEmits(['updateSelectedModules'])

const props = defineProps({
  display: Boolean,
  selectedModules: Object
});

const updateSelectedModules = (newValue) => {
    emit('updateSelectedModules', newValue)
}

</script>

<style scoped>
.drawer {
    display: none;
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    background-color: #F4F4F4;
    padding: 2rem;
}

.drawer.active {
  display: block;
}

.close {
  text-align: right;
}
</style>