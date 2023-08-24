<template>
  <v-col cols="3" :class="{active: props.display}" class="drawer">
    <div class="fixedDrawer v-col-3">
      <div class="pa-2 ma-2">
        <div class="close">
          <v-btn variant="text" icon="mdi-close" color="#CA8702" @click="$emit('toggle', false)"></v-btn>
        </div>


        <h2 class="mt-5 mb-5">Votre sélection</h2>
        <v-divider class="mb-10"></v-divider>

        <div v-for="(selectedModule, index) in selectedModules" :key="index">
          <ItemResultModule 
            @updateSelectedModules="updateSelectedModules"
            @updateCurrentModuleId="updateCurrentModuleId"
            :selectedModule="selectedModule"
            :selectedModules="selectedModules"
          />
        </div>

      </div>
    </div>
  </v-col>
</template>

<script setup>
import ItemResultModule from './ItemResultModule.vue';
import { defineProps } from 'vue';

const emit = defineEmits(['updateSelectedModules', 'updateCurrentModuleId'])

const props = defineProps({
  display: Boolean,
  selectedModules: Object
});

const updateSelectedModules = (newValue) => {
  emit('updateSelectedModules', newValue)
}

const updateCurrentModuleId = (newValue) => {
  emit('updateCurrentModuleId', newValue)
} 

</script>

<style scoped>
.drawer {
  display: none;
  background-color: #F4F4F4;
  padding: 2rem;
}

.drawer.active {
  display: block;
}

.fixedDrawer {
  position: fixed;
  right: 0;
  top: 0;
}
.close {
  text-align: right;
}
</style>