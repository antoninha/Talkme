<template>
  <v-row>
    <v-col cols="3">
      <v-sheet class="pa-2 ma-2">
        <Choice></Choice>
      </v-sheet>
    </v-col>

    <v-col cols="6">
      <v-sheet class="pa-2 ma-2">
        <v-row>
          <v-col
            v-for="(selectedModule, index) in selectedModules"
            :key="index"
            :cols="selectedModule.contentModule.double ? 12 : 6"
          >
            <ContainerModule :title="selectedModule.contentModule.label" :double="selectedModule.contentModule.double">
              <component :is="selectedModule.contentModule.component" />
            </ContainerModule>
          </v-col>
        </v-row>
      </v-sheet>
    </v-col>

    <v-col cols="3">
      <v-sheet class="pa-2 ma-2">
        <ResultConfiguration :selectedModules=selectedModules @updateSelectedModules="updateSelectedModules" />
      </v-sheet>
    </v-col> 
  </v-row>
</template>

<script setup>
import { ref } from "vue";
import ContainerModule from "@/components/modulesTool/ContainerModule.vue";
import BarModule from "@/components/modulesTool/BarModule.vue";
import DoughnutModule from "@/components/modulesTool/DoughnutModule.vue";
import ResultConfiguration from '@/components/modulesResult/ResultConfiguration.vue';
import Choice from '@/components/Choice.vue'

const updateSelectedModules = (newValue) => {
  selectedModules.value = newValue;
}

// const modules = ref([
//   {
//     id: 1,
//     title: "Commandes et ventes",
//     icon: "mdi-ticket-confirmation-outline",
//     color: "#1234AD",
//     contentModule: {
//         label: "Doughnut chart",
//         double: false,
//         component: DoughnutModule,
//       },
//   },
//   {
//     id: 2,
//     title: "Facturation",
//     icon: "mdi-file-document-outline",
//     color: "#707070",
//     contentModule: {
//         label: "Bar chart",
//         double: false,
//         component: BarModule,
//       },
//   },
//   {
//     id: 3,
//     title: "Production",
//     icon: "mdi-factory",
//     color: "#B1340C",
//     contentModule: {
//       label: "Gestion des commandes et des ventes",
//       double: true,
//       component: BarModule,
//     }
//   }
// ]);

const selectedModules = ref([
{
    id: 1,
    title: "Commandes et ventes",
    icon: "mdi-ticket-confirmation-outline",
    color: "#1234AD",
    contentModule: {
        label: "Doughnut chart",
        double: false,
        component: DoughnutModule,
      },
  },
  {
    id: 2,
    title: "Facturation",
    icon: "mdi-file-document-outline",
    color: "#707070",
    contentModule: {
        label: "Bar chart",
        double: false,
        component: BarModule,
      },
  },
]);
  
</script>

<style>
.container-icon {
  border-radius: 10px;
  background: #ffe3ac;
  padding: 10px;
}
</style>
