<template>
  <div class="text-center">
    <v-btn
      size="small"
      variant="outlined" 
      color="#CA8702"
      @click="openDialogAndReset"  
    >
      En savoir plus
    </v-btn>
    <v-dialog
      v-model="dialog"
      activator="parent"
      width="auto"
      maxWidth="60%"
    >
      <v-card class="d-flex flew-row px-7 py-7" v-if="page === 0">
        <v-card-text>
          <h1>{{item.title}}</h1>
          <p>{{item.completeDescription}}</p>
        </v-card-text>
        <v-img src="/assets/dialogImg.png" class="px-5" maxWidth="40rem"></v-img>
        <v-card-actions class="ml-4 py-5">
          <v-btn  variant="flat" color="#CA8702" class="text-white" @click="page++" :disabled="moduleIsAlreadySelected">
            Ajouter +
          </v-btn>
        </v-card-actions>
      </v-card>

      <div v-if="page === 1">
        <ChoiceContentModule 
          :item="item"
          :selectedModules="selectedModules"
          @updateSelectedModules="updateSelectedModules"
          @updateCurrentModuleId="updateCurrentModuleId"
        />
      </div>
    </v-dialog>
  </div>
</template>
<script setup>
  import { ref } from 'vue';
  import ChoiceContentModule from './ChoiceContentModule.vue';
  
  defineProps({
    item:Object,
    selectedModules: Object,
    moduleIsAlreadySelected: Object
  })

  const emit = defineEmits(['updateSelectedModules', 'updateCurrentModuleId'])

  const updateSelectedModules = (newValue) => {
    dialog.value = false;
    emit('updateSelectedModules', newValue)
  }

  const updateCurrentModuleId = (newValue) => {
    emit('updateCurrentModuleId', newValue)
  }

  const dialog = ref(false)
  const page = ref(0)

  const openDialogAndReset = () => {
    page.value = 0;
  }

</script>
