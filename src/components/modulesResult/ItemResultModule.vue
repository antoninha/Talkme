<template>
    <div
        class="d-flex align-center custom-card px-8 py-5 mb-5"
    >
        <v-btn class="remove" variant="text" icon="mdi-minus-circle" color="#D34949" @click="updateSelectedModules(props.selectedModule.id)"></v-btn>
        <v-icon :color=props.selectedModule.color :icon=props.selectedModule.icon class="mr-5"></v-icon>
        <p>{{ props.selectedModule.title }}</p>
    </div>    
</template>


<script setup>
    const props = defineProps(['selectedModule', 'selectedModules'])
    const emit = defineEmits(['updateSelectedModules', 'updateCurrentModuleId'])

    const updateSelectedModules = (idToRemove) => {
        const updatedData = props.selectedModules.filter(item => item.id !== idToRemove);
        const updateCurrentModuleId = updatedData.length ? updatedData[0].id : 0;
        emit('updateSelectedModules', updatedData)
        emit('updateCurrentModuleId', updateCurrentModuleId)
    }
</script>

<style scoped>
    .custom-card {
        box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.05);
        background-color: white;
        width: 100%;
        position: relative;
    }

    p {
        font-size: 1.1rem;
    }

    .remove {
        position: absolute;
        top: 0;
        right: 0;
        transform: translate(50%, -50%);
    }
</style>