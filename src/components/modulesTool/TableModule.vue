<template>
  <v-table>
    <thead>
      <tr>
        <th class="text-left">Nom</th>
        <th class="text-left">Prénom</th>
        <th class="text-left">Poste</th>
        <th class="text-left">Salaire</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in listeEmployes" :key="item.name">
        <td>{{ item.lastname }}</td>
        <td>{{ item.firstname }}</td>
        <td>{{ item.job }}</td>
        <td>{{ item.pay }}</td>
      </tr>
    </tbody>
  </v-table>
</template>

<script setup>
import { ref } from "vue";

const listeEmployes = ref([
  {
    lastname: "Doe",
    firstname: "John",
    job: "Ingénieur logiciel",
    pay: 75000,
  },
  {
    lastname: "Smith",
    firstname: "Alice",
    job: "Responsable des ventes",
    pay: 60000,
  },
  {
    lastname: "Johnson",
    firstname: "Bob",
    job: "Comptable",
    pay: 55000,
  },
  {
    lastname: "Williams",
    firstname: "Emily",
    job: "Analyste financier",
    pay: 65000,
  },
]);
</script>
