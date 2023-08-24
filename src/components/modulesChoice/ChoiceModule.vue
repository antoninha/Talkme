<template>
      <v-img
      :width="200"
      aspect-ratio="16/9"
      cover
      src="src\assets\logo.png"
      class="logo"
    ></v-img>

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
            <DialogInfo :item="moduleItem"></DialogInfo>

            <v-btn size="small" v-if="!moduleIsAlreadySelected(moduleItem.id)" variant="flat" color="#CA8702" class="text-white" @click="addSelectedModules(moduleItem)">
              Ajouter +
            </v-btn>

            <v-btn 
              size="small" 
              variant="flat" 
              color="#CA8702" 
              class="text-white" 
              v-if="moduleIsAlreadySelected(moduleItem.id)" 
              :disabled="isCurrentModule(moduleItem.id)" 
              @click="editCurrentModules(moduleItem)"
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

  const emit = defineEmits(['updateSelectedModules', 'updateCurrentModuleId'])

  const props = defineProps({
    modules: Object,
    selectedModules: Object,
    currentModuleId: Number,
  })

  const moduleIsAlreadySelected = (itemId) => {
    return props.selectedModules.some(selectedModule => selectedModule.id === itemId);
  };

  const addSelectedModules = (currentModule) => {
    const newSelectedModule = [...props.selectedModules, currentModule];
    emit('updateSelectedModules', newSelectedModule)
    emit('updateCurrentModuleId', currentModule.id)
  }

  const editCurrentModules = (currentModule) => {
    emit('updateCurrentModuleId', currentModule.id)
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