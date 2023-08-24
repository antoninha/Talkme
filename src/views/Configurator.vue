<template>
  <v-row>
    <v-col cols="3" class="choiceColumn">
      <v-sheet class="pa-2 ma-2" color="#F4F4F4">
        <ChoiceModule 
          :modules="modules" 
          :selectedModules=selectedModules 
          @updateSelectedModules="updateSelectedModules"
          @updateCurrentModuleId="updateCurrentModuleId"
        />
      </v-sheet>
    </v-col>

    <v-col cols="6">
      <v-sheet class="pa-2 ma-2" v-if="getCurrentModule()">
        <h2 class='pa-2 ma-2'>{{getCurrentModule().title}}</h2>
        <v-row>
          <v-col
            v-for="(contentModule, index) in getCurrentModule().contentModules"
            :key="index"
            :cols="contentModule.double ? 12 : 6"
          >
            <ContainerModule 
              :title="contentModule.label" 
              :double="contentModule.double" 
              :id="contentModule.id" 
              :currentModuleId="currentModuleId"
              :selectedModules=selectedModules
              @updateSelectedModules="updateSelectedModules"
            >
              <component :is="contentModule.component" />
            </ContainerModule>
          </v-col>
        </v-row>
      </v-sheet>
    </v-col>

    <v-col cols="3">
      <v-sheet class="pa-2 ma-2">
        <ResultConfiguration 
          :selectedModules=selectedModules 
          @updateSelectedModules="updateSelectedModules"  
        />
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
import ChoiceModule from '@/components/modulesChoice/ChoiceModule.vue'

const updateSelectedModules = (newValue) => {
  console.log(newValue);
  selectedModules.value = newValue;
  console.log(selectedModules.value);
}

const updateCurrentModuleId = (newValue) => {
  currentModuleId.value = newValue;
}

const getCurrentModule = () => {
  const currentModule = selectedModules.value.find(item => item.id === currentModuleId.value);
  return currentModule;
}

const selectedModules = ref([]);
const currentModuleId = ref();

const modules = ref([
  {
    id: 1,
    title: "Commandes et ventes",
    icon: "mdi-ticket-confirmation-outline",
    color: "#1234AD",
    description: "adadad",
    completeDescription:"Nisi eiusmod anim incididunt excepteur eu cupidatat do voluptate.",
    contentModules: [
      {
        id: 1,
        label: "lieu de livraison",
        double: false,
        component: DoughnutModule,
      },
      {
        id: 2,
        label: "Status de l'acheteur",
        double: false,
        component: DoughnutModule,
      },
      {
        id: 3,
        label: "Produits",
        double: true,
        component: BarModule,
      },
    ],
  },
  {
    id: 2,
    title: "Facturation",
    icon: "mdi-file-document-outline",
    color: "#707070",
    description: "adadad",
    completeDescription:"Nisi eiusmod anim incididunt excepteur eu cupidatat do voluptate.",
    contentModules: [
      {
        id: 1,
        label: "Evolution des factures",
        double: false,
        component: BarModule,
      },
      {
        id: 2,
        label: "Type de facture",
        double: false,
        component: DoughnutModule,
      }
    ],
  },
  {
    id: 3,
    title: "Production",
    icon: "mdi-factory",
    color: "#B1340C",
    description: "adadad",
    completeDescription:"Nisi eiusmod anim incididunt excepteur eu cupidatat do voluptate.",
    contentModules: [
        {
          id: 1,
          label: "Production machine 1",
          double: true,
          component: BarModule,
        },
        {
          id: 2,
          label: "Production machine 2",
          double: true,
          component: BarModule,
        },
        {
          id: 3,
          label: "Production machine 3",
          double: true,
          component: BarModule,
        },
        {
          id: 4,
          label: "Production machine 4",
          double: true,
          component: BarModule,
        }
    ]
  }
]);

</script>

<style>
.container-icon {
  border-radius: 10px;
  background: #ffe3ac;
  padding: 10px;
}

.choiceColumn {
  background-color: #F4F4F4;
  min-height: 100vh;
}
</style>
