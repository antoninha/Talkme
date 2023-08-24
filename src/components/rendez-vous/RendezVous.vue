<template>
  <div id="rendez-vous">
    <v-btn
      class="button-rendezVous"
    >
      Prendre rendez-vous

      <v-dialog
        v-model="dialog"
        activator="parent"
        width="auto"
      >
        <v-card class="rendez-vous">
          <div class="left">
            <img
              class="talkme-logo"
              src="../../assets/logo.png"
            />
            <div class="title">Rendez-vous audit</div>
            <div class="time">
              <span class="mdi mdi-clock-outline"></span>
              <div class="text-wrapper-35">15min</div>
            </div>

            <div class="google">
              <span class="mdi mdi-video-outline"></span>
              <div class="text-wrapper-78">Google Meet</div>
            </div>

            <p class="content">
              Démonstration en direct de la plateforme TM Factory, qui présente le
              tableau de bord de l'administrateur en amont.
            </p>
          </div>
          <div v-if="afficherDatePicker" class="calendar">
            <img src="./calendar.svg" alt="">
          </div>
          <div class="right" v-if="afficherDatePicker">
            <v-btn class="close" variant="text" icon="mdi-close" @click="dialog = false"></v-btn>
            <p>Vendredi 25 août 2023</p>
            <ul>
              <li>15:00</li>
              <li>15:15</li>
              <li>16:30</li>
            </ul>
            <v-btn class="suivant" @click="calendrierSuivant">Suivant</v-btn>
          </div>
          <div v-if="afficherFormulaire" class="form">
            <v-btn class="close" variant="text" icon="mdi-close" @click="dialogContent"></v-btn>
            <h2>Sélectionner un jour et une date</h2>
            <form>
              <div class="content">
                <label for="societe">Société</label>
                <input type="text" id="societe" v-model="societe" required>

                <label for="email">Email</label>
                <input type="email" id="email" v-model="email" required>

                <label for="secteur">Secteur d’activité</label>
                <input type="text" id="secteur" v-model="secteur" required>

                <label for="besoin"><span>* </span> Quel est votre besoin ?</label>
                <textarea id="besoin" v-model="besoin" required></textarea>
                <span style="margin-bottom: 45px;">* Facultatif</span>
              </div>

              <div class="btn-valider">
                <v-btn class="valider" @click="dialogContent">Valider</v-btn>
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
import { VDatePicker } from 'vuetify/labs/VDatePicker';

export default {
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
};
</script>

<style scoped>
.calendar{
  margin-top: 40px;
  margin-bottom: 40px;
}
.remove{
  display: none;
}
#rendez-vous{
  position: fixed;
  right: 30px;
  bottom: 30px;
}
.button-rendezVous{
  border-radius: 3px;
  background: #CA8702;
  display: flex;
  width: 100%;
  padding: 12px 14px;
  justify-content: center;
  align-items: center;
  font-weight: 600;
  color: white;
  text-transform: initial;
  margin-top: 20px;
  box-shadow: none;
  width: 253px;
}
.v-picker__header{
  display: none;
}
.rendez-vous{
  flex-direction: row !important;
}
.rendez-vous .left{
  max-width: 320px;
  padding: 40px;
}
.rendez-vous .left .title{
  font-size: 20px;
  font-weight: 600;
  margin-top: 40px;
}
.rendez-vous .left .time, .rendez-vous .left .google{
  display: flex;
}
.rendez-vous .left .time{
  margin-top: 24px;
}
.rendez-vous .left .google{
  margin-bottom: 24px;
}
.rendez-vous .left .time span, .rendez-vous .left .google span{
  margin-right: 10px;
}
.rendez-vous .left .content{
  text-align: justify;
}
.rendez-vous .right{
  padding: 40px;
}
.rendez-vous .right ul li:first-child{
  background-color: #CA8702;
  color: white;
  margin-top: 34px;
}
.rendez-vous .right p{
  margin-top: 50px;
}
.rendez-vous .right ul li{
  display: flex;
  width: 242px;
  height: 37.714px;
  padding: 12px 14px;
  justify-content: center;
  align-items: center;
  border-radius: 3px;
  border: 1px solid #CA8702;
  list-style: none;
  color: #CA8702;
  font-weight: 600;
  margin-top: 6px;
}
.rendez-vous .right .suivant{
  border-radius: 3px;
  background: #CA8702;
  display: flex;
  width: 100%;
  padding: 6px;
  justify-content: center;
  align-items: center;
  font-weight: 600;
  color: white;
  text-transform: initial;
  margin-top: 20px;
  max-width: 125px;
  position: absolute;
  bottom: 40px;
  right: 40px;
}
.rendez-vous .right .v-btn--icon.v-btn--density-default {
    width: 0;
    height: 0;
}
.talkme-logo{
  max-width: 230px;
}

/* Ceci est un commentaire dans la section style */
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
.form{
  padding-left: 50px;
  border-left: 1px solid #CDCDCD;
  margin-left: 20px;
  padding-right: 50px;
  padding-top: 50px;
}
.form form{
  display: flex;
}
.form span{
  color: #CA8702;
}
.form form input, .form form textarea {
  border-radius: 3px;
  border: 1px solid #B7B7B7;
  margin-top: 10px;
  margin-bottom: 23px;
}
.close{
  float: right;
  color:#CA8702;
  font-weight: bold;
}
.form .v-btn--icon.v-btn--density-default {
    width: 0;
    height: 0;
}

.form .valider{
  border-radius: 3px;
  background: #CA8702;
  display: flex;
  width: 100%;
  padding: 6px;
  justify-content: center;
  align-items: center;
  font-weight: 600;
  color: white;
  text-transform: initial;
  width: 125px;
}

.btn-valider{
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
  margin-left: 40px;
  margin-bottom: 45px;
}

</style>
