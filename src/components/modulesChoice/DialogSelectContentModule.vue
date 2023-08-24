<template>

    <v-btn size="small" variant="flat" color="#CA8702" class="text-white" @click="openDialog()">
        Ajouter +
    </v-btn>

    <v-dialog
        v-model="dialog"
        width="auto"
    >
        <ChoiceContentModule
            :item="item"
            :selectedModules="selectedModules"
            @updateSelectedModules="updateSelectedModules"
            @updateCurrentModuleId="updateCurrentModuleId"
        />
    </v-dialog>

</template>

<script setup>
    import { ref } from 'vue';
    import ChoiceContentModule from './ChoiceContentModule.vue';

    defineProps({
        item: Object,
        selectedModules: Object,
    })

    const emit = defineEmits(['updateSelectedModules', 'updateCurrentModuleId'])

    const dialog = ref(false)

    const openDialog = () => {
        dialog.value = true;
    }

    const updateSelectedModules = (newValue) => {
        dialog.value = false;
        emit('updateSelectedModules', newValue)
    }

    const updateCurrentModuleId = (newValue) => {
        emit('updateCurrentModuleId', newValue)
    }
</script>