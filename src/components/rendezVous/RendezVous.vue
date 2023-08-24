<template>
  <div id="rendez-vous">
    <v-btn
      variant="flat" color="#CA8702" class="text-white mt-10 mb-10" width="100%"
    >
      Prendre rendez-vous

      <v-dialog
        v-model="dialog"
        activator="parent"
        width="auto"
      >
        <v-card class="rendez-vous">
          <div class="left px-12 py-12">
            <img
              class="talkme-logo"
              src="/assets/logo.png"
            />
            <div class="title my-2">Rendez-vous audit</div>
            <div class="time my-2">
              <span class="mdi mdi-clock-outline mr-2"></span>
              <div class="text-wrapper-35">15min</div>
            </div>

            <div class="google my-2">
              <span class="mdi mdi-video-outline mr-2"></span>
              <div class="text-wrapper-78">Google Meet</div>
            </div>

            <p class="content">
              Démonstration en direct de la plateforme TM Factory, qui présente le
              tableau de bord de l'administrateur en amont.
            </p>
          </div>

          <div v-if="afficherDatePicker" >
            <div class='d-flex'>
              <div  class="calendar px-4 pt-12">
                <p class='titleSectionDate my-4'>Sélectionner un jour et une date</p>
                <v-locale-provider locale="fr">
                  <v-date-picker v-model="date"></v-date-picker>
                </v-locale-provider>
  
                <v-select
                  class="mt-10"
                  label="Fuseau horaire"
                  :items="['UTC+1 (10:00)', 'UTC+2 (11:00)', 'UTC+3 (12:00)', 'UTC+4 (13:00)', 'UTC+5 (14:00)', 'UTC+6 (15:00)']"
                  variant="outlined"
                />
              </div>
  
              <div class="right px-12 pt-12">
                <v-btn class="close" variant="text" icon="mdi-close" @click="dialog = false"></v-btn>
                <p v-if="!date">Sélectionner une date</p>
                <div v-if="date" class="selectedDate">
                  <p class="my-5">{{ formattedDate }}</p>
                  
                  <v-item-group selected-class="timeSelected">
                    <v-item
                      v-for="time in times"
                      :key="time"
                      v-slot="{ selectedClass, toggle }"
                    >
                      <v-chip
                        :class="selectedClass"
                        @click="toggle"
                        variant="outlined"
                        color="#CA8702"
                        class="customChips"
                      >
                        {{ time }}
                      </v-chip>
                    </v-item>
                  </v-item-group>
                </div>
              </div>
            </div>

            <div class="d-flex justify-end mr-10 pb-10">
              <v-btn variant="flat" color="#CA8702" class="text-white mt-10" @click="calendrierSuivant">
                Suivant
              </v-btn>
            </div>
          </div>
          

          <div v-if="afficherFormulaire" class="form my-15 mx-15">
            <v-btn class="close" variant="text" icon="mdi-close" @click="dialogContent"></v-btn>
            <form>
              <div class="content">
                <v-text-field label="Société" v-model="societe" required variant="outlined"></v-text-field>
                <v-text-field label="Email" v-model="email" required variant="outlined"></v-text-field>
                <v-text-field label="secteur" v-model="secteur" required variant="outlined"></v-text-field>
                <v-textarea label="Quel est votre besoin ?" v-model="besoin" variant="outlined"></v-textarea>
              </div>

              <div class="btn-valider">
                <v-btn variant="flat" color="#CA8702" class="text-white" @click="dialogContent">
                  Valider
                </v-btn>

              </div>
            </form>
          </div>
        </v-card>
      </v-dialog>
    </v-btn>
  </div>
</template>
<script>
import { ref } from 'vue';
import { VDatePicker } from 'vuetify/labs/VDatePicker'
import { DateTime } from "luxon";

export default {
  data() {
    return {
      date: null,
      times: ['11:00', '11:15', '11:30', '11:45', '12:00', '12:15', '12:30', '12:45', '13:00']
    };
  },
  components: {
    VDatePicker,
  },
  setup() {
    const dialog = ref(false);
    const afficherDatePicker = ref(true);
    const afficherFormulaire = ref(false);

    const calendrierSuivant = () => {
      afficherDatePicker.value = false;
      afficherFormulaire.value = true;
    };

    const dialogContent = () =>{
      dialog.value = false
      setTimeout(() => {
        afficherDatePicker.value = true;
        afficherFormulaire.value = false;
      }, 1000);
    }

    return {
      dialog,
      afficherDatePicker,
      afficherFormulaire,
      calendrierSuivant,
      dialogContent
    };
  },

  computed: {
    formattedDate() {
      if (this.date) {
        const date = new Date(this.date);
        const luxonDate = DateTime.fromJSDate(date, { zone: "Europe/Paris" })
        const formatted = luxonDate.toLocaleString(DateTime.DATE_FULL);

        return formatted.charAt(0).toUpperCase() + formatted.slice(1);
      }
      return '';
    },
  },
};
</script>

<style>
.calendar .v-picker-title, .calendar .v-picker__header{
  display: none;
}

.calendar .mdi-chevron-left, .calendar .mdi-chevron-right, .calendar .mdi-chevron-down {
  color: #CA8702;
}

.calendar .v-picker__body .v-btn--variant-text {
  opacity: 1;
}

.calendar .v-picker__body .v-date-picker-month .v-date-picker-month__day--selected .v-btn {
  color: #CA8702 !important; 
}

.calendar .v-date-picker-month .v-date-picker-month__day--selected .bg-surface-variant {
  background: transparent !important;
}
.selectedDate .v-item-group {
  display: flex;
  flex-direction: column;
}

.selectedDate .v-chip{
  display: flex;
  justify-content: center;
  border-radius: 5px;
  padding: 1.2rem;
  margin-bottom: 0.5rem;
}

.timeSelected .v-chip__content {
  color: white;
}


</style>

<style scoped>
.remove{
  display: none;
}

.rendez-vous{
  flex-direction: row !important;
}
.rendez-vous .left{
  max-width: 320px;
}
.rendez-vous .left .title{
  font-size: 20px;
  font-weight: 600;
}
.rendez-vous .left .time, .rendez-vous .left .google{
  display: flex;
}

.rendez-vous .left .content{
  text-align: justify;
}

.calendar {
  text-align: center;
}

.titleSectionDate {
  font-size: 1.2rem;
  font-weight: bold;  
}

.selectedDate {
  min-width: 13rem;
  text-align: center;
}

.timeSelected{
  background-color: #CA8702;
}

.talkme-logo{
  max-width: 230px;
}

.form form .content{
  display: flex;
  flex-direction: column;
  min-width: 464px;
}
.form h2{
  font-size: 20px;
  font-weight: 600;
  margin-bottom: 40px;
}

.btn-valider {
  display: flex;
  justify-content: flex-end;
}

.close{
  position: absolute;
  top: 0;
  right: 0;
  color:#CA8702;
  font-weight: bold;
}

</style>
