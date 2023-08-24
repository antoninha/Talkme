<template>
    <v-img
      :width="200"
      aspect-ratio="16/9"
      cover
      src="/assets/logo.png"
      class="logo mb-5 mt-5"
    />

  <div v-for="(moduleItem, index) in modules" :key=index>

    <v-expansion-panels class="pa-2" elevation="n-0" >
      <v-expansion-panel class="elevation-0">

        <v-expansion-panel-title class="panel-title">
          <v-icon :icon= moduleItem.icon class="mr-5" :color= moduleItem.color></v-icon>
          {{moduleItem.title}}
        </v-expansion-panel-title>

        <v-expansion-panel-text class="d-flex flex-column">
          <p class="my-3">{{moduleItem.description}}</p>
          <div class="d-flex justify-space-between flex-wrap">
            <DialogInfo 
              :item="moduleItem"
              :selectedModules="selectedModules"
              :moduleIsAlreadySelected="moduleIsAlreadySelected(moduleItem.id)"
              @updateSelectedModules="updateSelectedModules"
              @updateCurrentModuleId="updateCurrentModuleId"
            />

            <DialogSelectContentModule 
              v-if="!moduleIsAlreadySelected(moduleItem.id)"
              :item="moduleItem"
              :selectedModules="selectedModules"
              @updateSelectedModules="updateSelectedModules"
              @updateCurrentModuleId="updateCurrentModuleId"
            />
            
            <v-btn 
              size="small" 
              variant="flat" 
              color="#CA8702" 
              class="text-white" 
              v-if="moduleIsAlreadySelected(moduleItem.id)" 
              :disabled="isCurrentModule(moduleItem.id)" 
              @click="updateCurrentModuleId(moduleItem.id)"
            >
              Revisionner
            </v-btn>
          </div>
        </v-expansion-panel-text>

      </v-expansion-panel>
    </v-expansion-panels>
  </div>
</template>
  
<script setup>
import DialogInfo from './DialogInfo.vue';
import DialogSelectContentModule from './DialogSelectContentModule.vue';

  const emit = defineEmits(['updateSelectedModules', 'updateCurrentModuleId'])
  
  const props = defineProps({
    modules: Object,
    selectedModules: Object,
    currentModuleId: Number,
  })

  const moduleIsAlreadySelected = (itemId) => {
    return props.selectedModules.some(selectedModule => selectedModule.id === itemId);
  };

  const updateSelectedModules = (newValue) => {
      emit('updateSelectedModules', newValue)
  }

  const updateCurrentModuleId = (newValue) => {
      console.log(newValue);
      emit('updateCurrentModuleId', newValue)
  }

  const isCurrentModule = (moduleId) => {
    if (props.currentModuleId === moduleId) {
      return true;
    }else {
      return false;
    }
  }
</script>
  
<style>
  .v-expansion-panel-title .v-expansion-panel-title__overlay{
    background-color: transparent;
  }
  
  .v-expansion-panel-text {
    text-align: justify;
    border-top: 2px solid #F3F3F3;
  }

  .v-expansion-panel .v-expansion-panel__shadow {
    box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.05);
  }
  .logo{
    margin-left: auto;
    margin-right: auto;
  }
</style>