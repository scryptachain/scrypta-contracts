<template>
  <div class="home">
    <div class="main text-left">
      <div class="container">
        <h1>Entra all'interno del contratto<br><span style="font-size:16px">{{ $route.params.address }}</span></h1>
        <hr>
        <div v-if="!isBroadcasting">
          <b-field label="Il tuo nome">
            <b-input v-model="name"></b-input>
          </b-field>
          <b-field label="Il tuo cognome">
            <b-input v-model="surname"></b-input>
          </b-field>
          <b-button type="is-primary" size="is-large" style="width:100%" v-on:click="sendContactstoContract">INVIA LE INFORMAZIONI AL CONTRATTO</b-button>
        </div>
        <div v-if="isBroadcasting">
          Stai inviando correttamente le informazioni al contratto, puoi chiudere la pagina non appena il creatore del contratto ha ricevuto le informazioni.
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  const ScryptaCore = require('@scrypta/core')

  export default {
    name: 'Home',
    data(){ 
      return {
        scrypta: new ScryptaCore(true),
        address: '',
        wallet: '',
        isLoading: true,
        isBroadcasting: false,
        name: '',
        surname: ''
      }
    },
    async mounted() {
      const app = this
      app.wallet = await app.scrypta.returnDefaultIdentity()
      let SIDS = app.wallet.split(':')
      app.address = SIDS[0]
      let identity = await app.scrypta.returnIdentity(app.address)
      app.wallet = identity
      app.isLogging = false
      app.isLoading = false
    },
    methods: {
      sendContactstoContract(){
        const app = this
        app.scrypta.connectP2P()
        if(app.name !== '' && app.surname !== ''){
          app.$buefy.dialog.prompt({
            message: `Inserisci la password del wallet`,
            inputAttrs: {
              type: "password"
            },
            trapFocus: true,
            onConfirm: async password => {
              let key = await app.scrypta.readKey(password, app.wallet.wallet);
              if (key !== false) {
                app.isBroadcasting = true
                setInterval(async function(){
                  app.scrypta.broadcast(app.wallet.wallet, password, 'message', JSON.stringify({action: 'join', name: app.name, surname: app.surname, contract: app.$route.params.address, time: new Date()}))
                },3000)
              } else {
                app.$buefy.toast.open({
                  message: "Wrong password!",
                  type: "is-danger"
                });
              }
            }
          })
        }else{
          app.$buefy.toast.open({
              message: `Inserisci name e surname prima di inviare le informazioni al contratto`,
              type: 'is-danger'
          })
        }
      }
    }
  }
</script>