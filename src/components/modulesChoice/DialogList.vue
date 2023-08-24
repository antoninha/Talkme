<template>
    <v-dialog
        v-model="dialog"
        activator="parent"
        width="auto"
      >
        <v-card class="d-flex flew-row">
          <v-card-text>
            <h1>{{item.title}}</h1>
            <p>{{item.completeDescription}}</p>
          </v-card-text>
          <v-img src="src\assets\dialogImg.png" class="px-10"></v-img>
          <v-card-actions class="ml-4 py-5">
            <v-btn v-if="!moduleIsAlreadySelected(moduleItem.id)" variant="flat" color="#CA8702" class="text-white" @click="addSelectedModules(moduleItem)">
              Ajouter +
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
</template>

<script setup>

</script>