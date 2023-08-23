<template>
  <v-row>
    <v-col cols="3" class="choiceColumn">
      <v-sheet class="pa-2 ma-2" color="#F4F4F4">
        <ChoiceModule :modules="modules" :selectedModules=selectedModules @updateSelectedModules="updateSelectedModules"/>
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
            <ContainerModule 
              :title="selectedModule.contentModule.label" 
              :double="selectedModule.contentModule.double" 
              :id="selectedModule.id" 
              :selectedModules=selectedModules
              @updateSelectedModules="updateSelectedModules"
            >
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
import ChoiceModule from '@/components/modulesChoice/ChoiceModule.vue'

const updateSelectedModules = (newValue) => {
  selectedModules.value = newValue;
}

const modules = ref([
  {
    id: 1,
    title: "Commandes et ventes",
    icon: "mdi-ticket-confirmation-outline",
    color: "#1234AD",
    description: "adadad",
    completeDescription:"Nisi eiusmod anim incididunt excepteur eu cupidatat do voluptate.",
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
    description: "adadad",
    completeDescription:"Nisi eiusmod anim incididunt excepteur eu cupidatat do voluptate.",
    contentModule: {
        label: "Bar chart",
        double: false,
        component: BarModule,
      },
  },
  {
    id: 3,
    title: "Production",
    icon: "mdi-factory",
    color: "#B1340C",
    description: "adadad",
    completeDescription:"Nisi eiusmod anim incididunt excepteur eu cupidatat do voluptate.",
    contentModule: {
      label: "Gestion des commandes et des ventes",
      double: true,
      component: BarModule,
    }
  }
]);

const selectedModules = ref([
{
    id: 1,
    title: "Commandes et ventes",
    icon: "mdi-ticket-confirmation-outline",
    color: "#1234AD",
    description: "adadad",
    completeDescription:"Nisi eiusmod anim incididunt excepteur eu cupidatat do voluptate.",
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
    description: "adadad",
    completeDescription:"Nisi eiusmod anim incididunt excepteur eu cupidatat do voluptate.",
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

.choiceColumn {
  background-color: #F4F4F4;
  min-height: 100vh;
}
</style>
