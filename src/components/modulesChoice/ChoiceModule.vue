<template>
  <div v-for="(moduleItem, index) in modules" :key=index>
    <v-expansion-panels class="pa-2" elevation="n-0" >
      <v-expansion-panel class="elevation-0">

        <v-expansion-panel-title class="panel-title">
          <v-icon :icon= moduleItem.icon class="mr-5" :color= moduleItem.color></v-icon>
          {{moduleItem.title}}
        </v-expansion-panel-title>

        <v-expansion-panel-text class="d-flex flex-column">
          <p class="my-3">{{moduleItem.text}}</p>
          <div class="d-flex justify-space-between">
            <DialogInfo :item="moduleItem"></DialogInfo>

            <v-btn v-if="!moduleIsAlreadySelected(moduleItem.id)" variant="flat" color="#CA8702" class="text-white" @click="addSelectedModules(moduleItem)">
              Ajouter +
            </v-btn>
          </div>
        </v-expansion-panel-text>

      </v-expansion-panel>
    </v-expansion-panels>
  </div>
</template>
  
<script setup>
  import DialogInfo from './DialogInfo.vue';

  const emit = defineEmits(['updateSelectedModules'])

  const props = defineProps({
    modules: Object,
    selectedModules: Object
  })

  const moduleIsAlreadySelected = (itemId) => {
    return props.selectedModules.some(selectedModule => selectedModule.id === itemId);
  };

  const addSelectedModules = (currentModule) => {
    const newSelectedModule = [...props.selectedModules, currentModule];
    emit('updateSelectedModules', newSelectedModule)
}
</script>
  
<style>
  .v-expansion-panel-title .v-expansion-panel-title__overlay{
    background-color: transparent;
  }
  
  .v-expansion-panel-text {
    border-top: 2px solid #F3F3F3;
  }

  .v-expansion-panel .v-expansion-panel__shadow {
    box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.05);
  }
</style>