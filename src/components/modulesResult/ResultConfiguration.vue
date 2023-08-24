<template>
    <v-badge color="#CA8702" :content="selectedModules.length" class='btn-right-bar' :class="{active: !display}">
        <v-btn prepend-icon="mdi-cart-variant" variant="outlined" color="#CA8702" @click="toggleDisplay">
            Votre sélection
        </v-btn>
    </v-badge>


    <ResultDrawer 
        :display="display"
        :selectedModules=props.selectedModules
        @toggle="toggleDisplay"
        @updateSelectedModules="updateSelectedModules"
        @updateCurrentModuleId="updateCurrentModuleId"
    />

       
</template>


<script setup>
import { ref } from 'vue';
import ResultDrawer from './ResultDrawer.vue';

const display = ref(false)
const emit = defineEmits(['updateSelectedModules', 'forceReloadComponent', 'updateCurrentModuleId'])

const props = defineProps({
    selectedModules: Object,
    forceUpdate: Number
})

const toggleDisplay = (newValue) => {
    display.value = newValue;
    const updateComponent = props.forceUpdate + 1;
    emit('forceReloadComponent', updateComponent)
}

const updateSelectedModules = (newValue) => {
    emit('updateSelectedModules', newValue)
}

const updateCurrentModuleId = (newValue) => {
    emit('updateCurrentModuleId', newValue)
}

</script>

<style scoped>
.btn-right-bar {
    position: absolute;
    top: 2rem;
    right: 2rem;
    display: none;
}

.btn-right-bar.active{
    display: block;
}
</style>