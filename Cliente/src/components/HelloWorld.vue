<template>
<div >
  <div class="fondo">
    <br><br>
      <h2>Envie un mensaje: </h2>
      <input id="mensajes" type="text" placeholder="Escriba aqui: ">
      <br>
      <br>
      <button class="btn btn-success" id="mensaje" type="button"  @click="enviar(mensaje)">Enviar</button>
  </div>
</div>
</template>


<script>
import Ws from '@adonisjs/websocket-client'
const ws = Ws('ws://192.168.43.69:3333')
export default {
    async created() {
    this.initializeWs()
   
    },
    data(){
        return{
          chat : null,
          mensaje:"",
        }
    },
    methods: {
      enviar : async function(mensaje){
        mensaje=document.getElementById("mensajes").value;
      this.chat.emit('message',mensaje)
    },
    initializeWs: async function(){
      ws.connect();
      this.chat = ws.subscribe('chat');
      let chat = this.chat;
      chat.on('message', (event)=>{
          // eslint-disable-next-line
        console.log(event);
      })
     }
    }
  }
</script>
<style>
  .fondo{
    background-color: lavender;
  }
</style>