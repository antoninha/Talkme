<template>
  <v-row>
    <v-col cols="2">
      <v-sheet class="pa-2 ma-2">
        <p>Test</p>
      </v-sheet>
    </v-col>

    <v-col cols="8">
      <v-sheet class="pa-2 ma-2">
        <p>Test</p>
      </v-sheet>
    </v-col>

    <v-col cols="2">
      <v-sheet class="pa-2 ma-2">
        <p>Test</p>
        <chat-component></chat-component>
        <RendezVous></RendezVous>
      </v-sheet>
    </v-col>
  </v-row>
</template>

<script setup>
  import ChatComponent from '../components/chatbot/index.vue';
  import RendezVous from '../components/rendez-vous/index.vue'
</script>

<style></style>
