<template>
    <div class="text-center">
    <v-btn
        variant="outlined" 
        color="#CA8702">
    
        En savoir plus

      <v-dialog
        v-model="dialog"
        activator="parent"
        width="auto"
      >
        <v-card>
          <v-card-text>
            {{item.title}}
        </v-card-text>
          <v-card-actions>
            <v-btn color="primary" block @click="dialog = false">Close Dialog</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-btn>
  </div>
</template>
<script setup>
    import { ref } from 'vue';

    defineProps({
        item:Object
    })

    const dialog = ref(false)
  
</script>
