<template>
  <v-row>
    <v-col cols="3">
      <v-sheet class="pa-2 ma-2">
        <p>Test</p>
      </v-sheet>
    </v-col>

    <v-col cols="6">
      <v-sheet class="pa-2 ma-2">
        <p>Test</p>
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
  import ResultConfiguration from '@/components/result/ResultConfiguration.vue';
import { ref } from 'vue';

  const updateSelectedModules = (newValue) => {
    selectedModules.value = newValue;
  }

  // const modules = [
  //   {
  //     id: 1,
  //     title: "Commandes et ventes",
  //     icon: "mdi-ticket-confirmation-outline",
  //     color: "#1234AD"
  //   },
  //   {
  //     id: 2,
  //     title: "Facturation",
  //     icon: "mdi-file-document-outline",
  //     color: "#707070"
  //   },
  //   {
  //     id: 3,
  //     title: "Production",
  //     icon: "mdi-factory",
  //     color: "#B1340C"
  //   }
  // ];

  const selectedModules = ref([
  {
      id: 1,
      title: "Commandes et ventes",
      icon: "mdi-ticket-confirmation-outline",
      color: "#1234AD"
    },
    {
      id: 2,
      title: "Facturation",
      icon: "mdi-file-document-outline",
      color: "#707070"
    }
  ]);


</script>

<style></style>
