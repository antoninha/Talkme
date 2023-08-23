<template>
  <v-row>
    <v-col cols="2">
      <v-sheet class="pa-2 ma-2">
        <p>Test</p>
      </v-sheet>
    </v-col>

    <v-col cols="8">
      <v-sheet class="pa-2 ma-2">
        <v-row>
          <v-col
            v-for="(module, index) in modules"
            :key="index"
            :cols="module.double ? 12 : 6"
          >
            <ContainerModule :title="module.label" :double="module.double">
              <component :is="module.component" />
            </ContainerModule>
          </v-col>
        </v-row>
      </v-sheet>
    </v-col>

    <v-col cols="2">
      <v-sheet class="pa-2 ma-2">
        <p>Test</p>
      </v-sheet>
    </v-col>
  </v-row>
</template>

<script setup>
import { ref } from "vue";
import ContainerModule from "@/components/modulesTool/ContainerModule.vue";
import BarModule from "@/components/modulesTool/BarModule.vue";
import DoughnutModule from "@/components/modulesTool/DoughnutModule.vue";

const modules = ref([
  {
    label: "Gestion des commandes et des ventes",
    double: true,
    component: BarModule,
  },
  {
    label: "Bar chart",
    double: false,
    component: BarModule,
  },
  {
    label: "Doughnut chart",
    double: false,
    component: DoughnutModule,
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
