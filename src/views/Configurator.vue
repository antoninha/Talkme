<template>
  <Tutorials />

  <v-row>
    <v-col cols="3" class="choiceColumn">
      <v-sheet class="pa-2 ma-2" color="#F4F4F4">
        <ChoiceModule
          :modules="modules"
          :selectedModules="selectedModules"
          :currentModuleId="currentModuleId"
          @updateSelectedModules="updateSelectedModules"
          @updateCurrentModuleId="updateCurrentModuleId"
        />
      </v-sheet>
    </v-col>

    <v-col :key="forceUpdate">
      <v-sheet class="pa-2 ma-2" v-if="getCurrentModule()">
        <h2 class="pa-2 ma-2">{{ getCurrentModule().title }}</h2>
        <v-row>
          <v-col
            v-for="(contentModule, index) in getCurrentModule().contentModules"
            :key="index"
            :cols="contentModule.double ? 12 : 6"
          >
            <ContainerModule
              :title="contentModule.label"
              :double="contentModule.double"
              :id="contentModule.id"
              :currentModuleId="currentModuleId"
              :selectedModules="selectedModules"
              @updateSelectedModules="updateSelectedModules"
            >
              <component :is="contentModule.component" />
            </ContainerModule>
          </v-col>
        </v-row>
        <AddNewModule
          class="mt-6"
          :currentModuleId="currentModuleId"
          :selectedModules="selectedModules"
          @updateSelectedModules="updateSelectedModules"
        />
      </v-sheet>
    </v-col>

    <ResultConfiguration
      :selectedModules="selectedModules"
      :forceUpdate="forceUpdate"
      @updateSelectedModules="updateSelectedModules"
      @forceReloadComponent="forceReloadComponent"
      @updateCurrentModuleId="updateCurrentModuleId"
    />
  </v-row>

  <ChatComponent />
</template>

<script setup>
import { ref } from "vue";
import ContainerModule from "@/components/modulesTool/ContainerModule.vue";
import BarModule from "@/components/modulesTool/BarModule.vue";
import DoughnutModule from "@/components/modulesTool/DoughnutModule.vue";
import ResultConfiguration from "@/components/modulesResult/ResultConfiguration.vue";
import ChoiceModule from "@/components/modulesChoice/ChoiceModule.vue";
import TableModule from "@/components/modulesTool/TableModule.vue";
import StatsModule from "@/components/modulesTool/StatsModule.vue";
import AddNewModule from "@/components/modulesTool/AddNewModule.vue";
import Tutorials from "@/components/tutorials/Tutorials.vue";
import ChatComponent from '../components/chatbot/Chatbot.vue';

const updateSelectedModules = (newValue) => {
  selectedModules.value = newValue;
};

const forceReloadComponent = (newValue) => {
  forceUpdate.value = newValue;
};

const updateCurrentModuleId = (newValue) => {
  currentModuleId.value = newValue;
};

const getCurrentModule = () => {
  const currentModule = selectedModules.value.find(
    (item) => item.id === currentModuleId.value
  );
  return currentModule;
};

const selectedModules = ref([]);
const currentModuleId = ref();
const forceUpdate = ref(0);

const modules = ref([
  {
    id: 1,
    title: "Commandes et ventes",
    icon: "mdi-ticket-confirmation-outline",
    color: "#1234AD",
    description:
      "Le module de commandes et de ventes constitue le pivot central de toute entreprise, permettant aux clients de passer aisément des commandes tout en fournissant aux équipes commerciales les outils nécessaires pour gérer efficacement les ventes, des premières sélections à la livraison finale.",
    completeDescription:
      "Le module de commandes et de ventes est le cœur battant de toute entreprise axée sur la commercialisation de produits ou de services. Il agit comme un chef d'orchestre, coordonnant les interactions cruciales entre les clients et l'entreprise. Doté de fonctionnalités puissantes, ce module simplifie et optimise le processus de vente du début à la fin. Du côté des commandes, ce module offre une interface intuitive permettant aux clients de passer des commandes en quelques clics. Grâce à des formulaires conviviaux, les clients peuvent choisir parmi une gamme de produits ou de services, spécifier leurs préférences et quantités, et ajouter les articles à leur panier virtuel. Une fois leurs sélections faites, le module affiche un récapitulatif clair avant que les clients ne finalisent leur commande. En ce qui concerne les ventes, le module permet aux équipes commerciales de suivre les commandes de manière efficace. Il offre des fonctionnalités pour gérer les stocks en temps réel, traiter les paiements de manière sécurisée et assurer le suivi des expéditions. Grâce à des tableaux de bord détaillés, les responsables peuvent surveiller les performances de vente, identifier les tendances et prendre des décisions éclairées pour stimuler la croissance.",
    contentModules: [
      {
        id: 1,
        label: "Lieu de livraison",
        double: false,
        component: DoughnutModule,
      },
      {
        id: 2,
        label: "Status de l'acheteur",
        double: true,
        component: TableModule,
      },
      {
        id: 3,
        label: "Produits",
        double: true,
        component: BarModule,
      },
    ],
  },
  {
    id: 2,
    title: "Facturation",
    icon: "mdi-file-document-outline",
    color: "#707070",
    description:
      "Le module de facturation, au cœur de la gestion financière, simplifie le processus crucial de création et d'envoi de factures. En automatisant cette tâche, il permet aux entreprises de maintenir un suivi précis des transactions, de garantir la conformité aux normes comptables et d'assurer des paiements ponctuels.",
    completeDescription:
      "Le module de facturation se révèle être l'épine dorsale de la gestion financière au sein de toute entreprise. Il se charge efficacement de la création, de l'envoi et du suivi des factures, allégeant ainsi le fardeau administratif et assurant une gestion comptable fluide. Grâce à une interface intuitive, les utilisateurs peuvent générer rapidement des factures précises en saisissant les détails pertinents tels que les produits ou services fournis, les tarifs correspondants et les informations de contact du client. L'automatisation offerte par le module de facturation va bien au-delà de la simple génération de factures. Il permet la personnalisation des modèles de factures pour refléter l'identité visuelle de l'entreprise, renforçant ainsi la cohérence de la marque. De plus, le suivi des factures en temps réel permet de garder un œil vigilant sur les paiements en attente, contribuant ainsi à maintenir une trésorerie saine. En fin de compte, le module de facturation offre bien plus qu'une simple gestion de documents financiers. Il incarne l'efficacité opérationnelle en minimisant les erreurs humaines, en accélérant les processus de paiement et en fournissant une vue d'ensemble précise de la santé financière de l'entreprise. Grâce à sa capacité à rationaliser les flux de travail liés à la facturation, ce module libère du temps et des ressources précieuses, permettant ainsi aux entreprises de se concentrer sur leur croissance et leur succès à long terme.",
    contentModules: [
      {
        id: 1,
        label: "Evolution des factures",
        double: false,
        component: BarModule,
      },
      {
        id: 2,
        label: "Type de facture",
        double: false,
        component: DoughnutModule,
      },
      {
        id: 3,
        label: "Statistique des commandes",
        double: true,
        component: StatsModule,
      },
    ],
  },
  {
    id: 3,
    title: "Production",
    icon: "mdi-factory",
    color: "#B1340C",
    description:
      "Le module de production agit comme le chef d'orchestre des opérations de fabrication, orchestrant efficacement chaque étape du processus pour garantir une production fluide et optimisée.",
    completeDescription:
      "Le module de production se révèle être le moteur central de toute opération de fabrication. Il orchestre efficacement le processus de production, depuis la planification initiale jusqu'à la livraison finale, assurant ainsi une gestion transparente et optimisée de chaque étape. En offrant une interface conviviale, ce module permet aux équipes de planification de créer et de gérer des ordres de production en fonction des commandes clients et des niveaux de stock. Grâce à des fonctionnalités avancées de suivi des matières premières et des ressources, il garantit une allocation optimale des ressources tout en minimisant les retards et les coûts. L'automatisation joue un rôle crucial dans le module de production en rationalisant les processus répétitifs tels que la génération de rapports d'état de la production, les mises à jour des niveaux de stock et la coordination des tâches entre les différentes équipes. Cette automatisation non seulement accélère la production, mais réduit également les risques d'erreurs humaines. En somme, le module de production est bien plus qu'un simple gestionnaire d'opérations de fabrication. Il incarne l'efficacité opérationnelle en optimisant les ressources, en accélérant les délais de production et en garantissant la qualité des produits finaux. Grâce à cette gestion transparente et coordonnée, les entreprises peuvent satisfaire les demandes des clients de manière fiable tout en maintenant une rentabilité optimale.",
    contentModules: [
      {
        id: 1,
        label: "Production machine 1",
        double: false,
        component: BarModule,
      },
      {
        id: 2,
        label: "Production machine 2",
        double: false,
        component: BarModule,
      },
      {
        id: 3,
        label: "Production machine 3",
        double: true,
        component: BarModule,
      },
      {
        id: 4,
        label: "Production machine 4",
        double: true,
        component: BarModule,
      },
    ],
  },
]);
</script>

<style>
.container-icon {
  border-radius: 10px;
  background: #ffe3ac;
  padding: 10px;
}

.choiceColumn {
  background-color: #f4f4f4;
  min-height: 100vh;
}
</style>
