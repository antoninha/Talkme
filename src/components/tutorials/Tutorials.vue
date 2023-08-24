<template>
    <div class="text-center">
        <v-dialog
            v-model="dialog"
            width="auto"
            max-width="50%"
        >
            <v-card v-if="page === 0">
                <v-card-title>
                    Bienvenue sur TM FACTORY ! 
                </v-card-title>
                <v-card-text>
                    <p>Notre ERP personnalisable qui s’adapte à vos besoins !</p>
                    <br />
                    <p>TM FACTORY vous permet de créer votre propre espace de gestion d’entreprise en
                    intégrant l’ensemble de ses fonctions, dont la gestion des ressources humaines, la
                    gestion comptable et financière, l'aide à la décision, mais aussi la vente, la distribution,
                    l'approvisionnement et le commerce électronique.</p>
                    <br />
                    <ul>
                        <li>
                            Veuillez sélectionner en <span class="yellow">cliquant</span> sur les modules que vous souhaitez retrouver sur le
                            <span class="yellow">panneau latéral de gauche</span>. Ainsi, vous en saurez plus sur ce dernier et vous aurez le
                            choix entre <span class="yellow">en savoir plus</span> et <span class="yellow">l’ajouter</span>.
                        </li>
                    </ul>
                </v-card-text>
                <v-card-actions class="justify-end">
                    <v-btn color="#fff" append-icon="mdi-chevron-right" @click="page++">Suivant</v-btn>
                </v-card-actions>
            </v-card>

            <v-card v-if="page === 1">
                <v-card-text>
                    <p>Vous aurez deux choix face à vous : <span class="yellow">En savoir plus</span> et <span class="yellow">Ajouter +</span></p>
                    <br />
                    <ul>
                        <li>
                            <span class="yellow">En savoir plus :</span> vous en découvrirez toutes les spécificités, les détails et ce que ce module peut apporter à votre ERP personnalisable.
                        </li>
                        <li>
                            <span class="yellow">Ajouter :</span>Vous aurez les détails des sous-modules inhérent à ce dernier et de faire un choix.
                        </li>
                    </ul>
                    <br />
                    <p>Après avoir fait votre choix, votre module s’affichera au milieu de votre page et un <span class="yellow">bandeau latéral droit</span> s’affichera. Ce dernier vous affichera votre sélection actuel en plus de vous proposer un rendez-vous avec un de nos professionnels pour une demande de devis.</p>
                </v-card-text>
                <v-card-actions class="justify-space-between">
                    <v-btn color="#CA8702" variant="outlined" prepend-icon="mdi-chevron-left" @click="page--">Précédent</v-btn>
                    <v-btn color="#fff" append-icon="mdi-chevron-right" @click="page++">Suivant</v-btn>
                </v-card-actions>
            </v-card>

            <v-card v-if="page === 2">
                <v-card-title>
                    Bonne visite sur notre ERP !
                </v-card-title>
                <v-card-text>
                    <p>Nous espérons qu’après cette démo notre solution vous aura séduite !</p>
                </v-card-text>
                <v-card-actions class="justify-space-between">
                    <v-btn color="#CA8702" variant="outlined" prepend-icon="mdi-chevron-left" @click="page--">Précédent</v-btn>
                    <v-btn color="#fff" append-icon="mdi-chevron-right" @click="dialog = false">Suivant</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </div>
</template>


<script setup>
    import { ref } from 'vue';

    const dialog = ref(true)
    const page = ref(0)
</script>

<style scoped>
    .v-card {
        padding: 2rem;
        border-radius: 1rem;
    }

    .v-card-title {
        font-weight: bold;
    }

    ul {
        padding-left: 1.5rem;
    }

    .yellow {
        color: #CA8702;
    }

    .v-btn {
        padding: 0.8rem 1.5rem;
        height: auto;
    }

    .v-btn--variant-text {
        background-color: #CA8702;
    }
</style>