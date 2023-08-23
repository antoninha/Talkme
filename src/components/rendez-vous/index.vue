<template>
  <div>
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
              src="https://generation-sessions.s3.amazonaws.com/5b314dc6cdeddd86d8f74f44afd8cae4/img/talkme-logo-2@2x.png"
            />
            <div class="title">Rendez-vous audit</div>
            <div class="time">
              <img
              src="https://generation-sessions.s3.amazonaws.com/5b314dc6cdeddd86d8f74f44afd8cae4/img/clock.svg"
              />
              <div class="text-wrapper-35">15min</div>
            </div>

            <div class="google">
              <img
              class="vector-12"
              src="https://generation-sessions.s3.amazonaws.com/5b314dc6cdeddd86d8f74f44afd8cae4/img/vector.svg"
              />
              <div class="text-wrapper-78">Google Meet</div>
            </div>

            <p class="content">
              Démonstration en direct de la plateforme TM Factory, qui présente le
              tableau de bord de l'administrateur en amont.
            </p>
          </div>
          <v-date-picker></v-date-picker>
          <div class="right">
            <button class="close" @click="dialog = false">X</button>
            <p>Vendredi 25 août 2023</p>
            <ul>
              <li>15:00</li>
              <li>15:15</li>
              <li>16:30</li>
            </ul>
            <button class="suivant">Suivant</button>
          </div>
        </v-card>
      </v-dialog>
    </v-btn>
  </div>
</template>
<script>
import { VDatePicker } from 'vuetify/labs/VDatePicker'

  export default {
    components: {
      VDatePicker,
    },
    data () {
      return {
        dialog: false,
      }
    },
  }
</script>

<style scoped>
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
.rendez-vous .left .time img, .rendez-vous .left .google img{
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
.rendez-vous .right .close{
  float: right;
  color:#CA8702;
  font-weight: bold;
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
.talkme-logo{
  max-width: 230px;
}
</style>
