<template>
  <div v-for="(moduleItem, index) in modules" :key=index>
    <v-expansion-panels class="pa-2" elevation="n-0" >
      <v-expansion-panel 
       class="elevation-0">
       
        <v-expansion-panel-title class="panel-title">
          <v-icon :icon= moduleItem.icon class="mr-5" :color= moduleItem.color></v-icon>
          {{moduleItem.title}}
        </v-expansion-panel-title>
        <v-expansion-panel-text class="d-flex flex-column">
          <p class="my-3">{{moduleItem.text}}</p>
          <div class="d-flex justify-space-between">
            <DialogInfo :item="moduleItem"></DialogInfo>

            <v-btn variant="flat" color="#CA8702" class="text-white">
              Ajouter +
            </v-btn>
          </div>
        </v-expansion-panel-text>

      </v-expansion-panel>
    </v-expansion-panels>
  </div>
</template>
  
<script setup>
  import DialogInfo from '@/components/DialogInfo.vue'
    const modules = [
    {
      title: "Commandes et ventes",
      icon: "mdi-ticket-confirmation-outline",
      color: "#1234AD",
      description: "adadad",
      completeDescription:"Nisi eiusmod anim incididunt excepteur eu cupidatat do voluptate."
    },
    {
      title: "Facturation",
      icon: "mdi-file-document-outline",
      color: "#707070",
      text: "dadasdkdkada"
    },
    {
      title: "Production",
      icon: "mdi-factory",
      color: "#B1340C",
      text: "przoorkze"
    }
]

</script>
  
<style>
    .v-expansion-panel-title .v-expansion-panel-title__overlay{
    background-color: transparent;
  }
  
  .v-expansion-panel-text {
    border-top: 2px solid #F3F3F3;
  }

  .v-expansion-panel .v-expansion-panel__shadow {
    box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.05);
  }
</style>