<template>
  <v-card class="px-8 py-8">
    <v-card-text class="selectContentModule">
      <h1>{{ item.title }}</h1>
      <br />
      <p>Sélectionnez les éléments que vous souhaitez retrouver dans votre ERP.</p>
      <br />
      <div v-for="(contentModule, index) in item.contentModules" :key="index">
        <v-checkbox
          v-model="contentModuleSelected"
          :label="contentModule.label"
          :value="contentModule.id"
          color="#CA8702"
        />
      </div>
    </v-card-text>
    <v-card-actions class="ml-4 py-5">
      <v-btn variant="flat" color="#CA8702" class="text-white" @click="submitAndClose()">
        Ajouter +
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script setup>
  import { ref } from 'vue';

  const props = defineProps({
    item:Object,
    selectedModules: Object
  })

  const emit = defineEmits(['updateSelectedModules', 'updateCurrentModuleId'])

  const contentModuleSelected = ref([])

  const submitAndClose = () => {
    const filteredContentModules = props.item.contentModules.filter(contentModule => contentModuleSelected.value.includes(contentModule.id));

    const modifiedSelectedModule = {
      ...props.item,
      contentModules: filteredContentModules
    };

    const newSelectedModule = [...props.selectedModules, modifiedSelectedModule];

    emit('updateSelectedModules', newSelectedModule)
    emit('updateCurrentModuleId', modifiedSelectedModule.id)
  }

</script>

<style>

.selectContentModule .v-checkbox .v-selection-control {
  min-height: auto;
}

.selectContentModule .v-input__details {
  display: none;
}
</style>