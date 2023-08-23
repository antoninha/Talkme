<template>
    <div>
        <v-badge color="#CA8702" :content="selectedModules.length">
            <v-btn prepend-icon="mdi-cart-variant" variant="outlined" color="#CA8702" @click="toggleDisplay">
                Votre sélection
            </v-btn>
        </v-badge>
        
        <ResultDrawer @toggle="toggleDisplay" @updateSelectedModules="updateSelectedModules" :display="display" :selectedModules=props.selectedModules />
  </div> 
</template>


<script setup>
import { ref } from 'vue';
import ResultDrawer from './ResultDrawer.vue';

const display = ref(false)
const emit = defineEmits(['updateSelectedModules'])

const props = defineProps({
    selectedModules: Object
})

const toggleDisplay = (newValue) => {
    display.value = newValue;
}

const updateSelectedModules = (newValue) => {
    emit('updateSelectedModules', newValue)
}

</script>