<template>
  <div class="chat-container  v-col-2">
    <v-btn class="chat-button" variant="text" icon="mdi-chat-outline" @click="toggleChat"></v-btn>
    <div v-if="chatOpen" class="chat-window">
      <div class="chat-header">
        <div class="chat-header-left">
          <img src="/assets/bot.svg" />
          <div class="chat-header-text">
            <span>Léon Bot</span>
            <span>En ligne</span>
          </div>
        </div>
        <button class="close-button" @click="closeChat">-</button>
      </div>
      <div class="chat-messages">
        <div v-for="message in messages" :key="message.id">
          <span v-if="message.type === 'answer'" class="bot">
            <img src="/assets/bot.svg" />
            Léon bot
          </span>
          <div  :class="['message', message.type]">
            {{ message.text }}
          </div>
        </div>
      </div>
      <div class="chat-input">
        <input v-model="inputMessage" @keyup.enter="sendMessage" placeholder="Entrez votre question..." />
        <v-btn class="button" variant="text" icon="mdi-send" @click="sendMessage"></v-btn>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted  } from 'vue';

export default {
  setup() {
    const chatOpen = ref(false);
    const inputMessage = ref('');
    const messages = ref([]);

    const toggleChat = () => {
      chatOpen.value = !chatOpen.value;
      // Masquer le bouton "Prendre rendez-vous" au clic
      if (chatOpen.value) {
        chatButton.classList.add('hidden');
      }
    };

    const closeChat = () => {
      chatOpen.value = false;
       // Réafficher le bouton "Prendre rendez-vous" lorsque le tchat est fermé
       chatButton.classList.remove('hidden');
    };

    const sendMessage = () => {
      if (inputMessage.value.trim() !== '') {
        messages.value.push({ text: inputMessage.value, type: 'question' });

        let predefinedAnswer = 'a';

        if (inputMessage.value.includes('quelle technologie utilisez vous ?')) {
          predefinedAnswer = 'Nous utilisons Vue.js pour notre application.';
        } else if (inputMessage.value.includes('à quoi sert la solution proposée ?')) {
          predefinedAnswer = 'TM FACTORY apporte du lien entre vos outils et vos collaborateurs. Il centralise d’un côté les données de vos logiciels et de l’autre celles de vos machines.';
        } else {
          predefinedAnswer = "Je ne comprend pas votre question.";
        }

        messages.value.push({ text: predefinedAnswer, type: 'answer' });

        inputMessage.value = '';
      }
    };

    // Référence au bouton "Prendre rendez-vous" pour le masquer
    let chatButton = null;

    // Attendre que le composant soit monté pour obtenir la référence au bouton
    onMounted(() => {
      chatButton = document.querySelector('.chat-button');
    });

    return {
      chatOpen,
      inputMessage,
      messages,
      toggleChat,
      closeChat,
      sendMessage
    };
  },
};
</script>


<style scoped>
.bot{
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}
.bot img{
 margin-right: 5px;
}
.question{
  margin-top: 10px;
  margin-bottom: 10px;
}
.chat-container {
  position: fixed;
  right: 30px;
  bottom: 8rem;
  padding: 0;
}
.chat-button {
  cursor: pointer;
  border-radius: 3px;
  background: #CA8702;
  display: flex;
  width: 3rem;
  height:3rem;
  padding: 6px;
  justify-content: center;
  align-items: center;
  font-weight: 600;
  color: white;
  text-transform: initial;
  border-radius: 100%;
  float: right;
}
.chat-button.hidden {
  display: none; /* Masquer lorsque la classe hidden est ajoutée */
}
.chat-window {
  width: 100%;
  height: 350px;
  display: flex;
  flex-direction: column;
  border-radius: 10px;
  background: #ECE4D5;
  box-shadow: 0px 0px 20px 0px rgba(0, 0, 0, 0.10);
  overflow: hidden;
}
.chat-header {
  padding: 10px;
  background: #CA8702;
  color: white;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 14px;
  font-style: normal;
  font-weight: 500;
}
.chat-header-left{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.chat-header-text{
  display: flex;
  flex-direction: column;
  margin-left: 20px;
}
.chat-header-text span:nth-child(2){
  font-size: 12px;
}
.close-button{
  font-size: 20px;
  font-weight: bold;
}
.chat-messages {
  flex: 1;
  padding: 10px;
  overflow-y: auto;
}
.message {
  margin-bottom: 10px;
}

.chat-input{
  display: flex;
  outline: none;
  border-top: 1px solid #C0C0C0;;
}
.chat-input input{
  padding: 10px;
  display: flex;
  background-color: white;
  outline: none;
  width: 80%;
}

.chat-input .button{
  width: 20%;
  background-color: white;
  border-radius: 0;
  color: #CA8702;
  height: 100%;
}

/* Style pour les questions de l'utilisateur */
.message.question {
  margin-left: auto;
  border-radius: 10px;
  align-self: flex-end;
  max-width: 80%;
  padding: 10px;
  background-color: white;
  border: 1px solid #CA8702;
}

/* Style pour les réponses */
.message.answer {
  margin-right: auto;
  border-radius: 0px 10px 10px 10px;
  padding: 10px;
  align-self: flex-start;
  max-width: 80%;
  background-color: white;
}


</style>
