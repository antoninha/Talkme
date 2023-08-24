<template>
  <div>
    <v-btn @click="dialog = true" prepend-icon="mdi-plus">
      Ajouter un module
    </v-btn>
    <v-dialog v-model="dialog" width="600">
      <v-card>
        <v-form ref="form">
          <p class="text-h6 ml-4 mt-2">Créer votre module personnalisé :</p>
          <v-container class="d-flex flex-column">
            <v-text-field
              label="Nom du module"
              required
              variant="outlined"
              v-model="formInfo.label"
            ></v-text-field>
            <v-select
              label="Type de module"
              :items="existingModules"
              variant="outlined"
              item-value="id"
              item-title="label"
              v-model="formInfo.moduleSelected"
              required
            ></v-select>
            <v-checkbox
              v-model="formInfo.moduleDouble"
              label="Module double"
            ></v-checkbox>
          </v-container>
        </v-form>
        <v-card-actions class="d-flex justify-end">
          <v-btn @click="dialog = false">Fermer</v-btn>
          <v-btn
            :disabled="disabledBtn"
            color="primary"
            @click="addContentModule"
            >Créer mon module</v-btn
          >
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";
import BarModule from "@/components/modulesTool/BarModule.vue";
import DoughnutModule from "@/components/modulesTool/DoughnutModule.vue";
import StatsModule from "@/components/modulesTool/StatsModule.vue";
import TableModule from "@/components/modulesTool/TableModule.vue";

const form = ref(null);
const dialog = ref(false);
const formInfo = ref({
  label: "",
  moduleSelected: null,
  moduleDouble: false,
});
const disabledBtn = ref(true);

watch(formInfo.value, (info) => {
  if (!info.label || !info.moduleSelected) return;
  disabledBtn.value = false;
});

const emit = defineEmits(["updateSelectedModules"]);

const props = defineProps({
  currentModuleId: Number,
  selectedModules: Object,
});

function addContentModule() {
  const newSelectedModule = props.selectedModules.map((selectedModule) => {
    if (selectedModule.id === props.currentModuleId) {
      return {
        ...selectedModule,
        contentModules: [
          ...selectedModule.contentModules,
          {
            id: Math.floor(Math.random() * 100),
            label: formInfo.value.label,
            double: formInfo.value.moduleDouble,
            component: existingModules.value.find(
              (module) => module.id === formInfo.value.moduleSelected
            ).component,
          },
        ],
      };
    }
    return selectedModule;
  });

  emit("updateSelectedModules", newSelectedModule);
  dialog.value = false;
  disabledBtn.value = true;
  form.value.reset();
}

const existingModules = ref([
  { id: 1, label: "Graphique en bar", component: BarModule },
  { id: 2, label: "Graphique en camenbert", component: DoughnutModule },
  { id: 3, label: "Statistiques", component: StatsModule },
  { id: 4, label: "Tableau", component: TableModule },
]);
</script>
