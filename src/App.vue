<template>
  <div id="app">
    <v-app>
      <v-banner
        color="info"
        dark
        class="text-left"
      >
        Get our free app. It won't take up space on your phone and also works offline!
        
        <template v-slot:actions>
          <v-btn text @click="dismiss">Dismiss</v-btn>
          <v-btn text @click="install">Install</v-btn>
        </template>
      </v-banner>

      <v-banner
        v-if="deferredPrompt"
        color="info"
        dark
        class="text-left"
      >
        Get our free app. It won't take up space on your phone and also works offline!
        
        <template v-slot:actions>
          <v-btn text @click="dismiss">Dismiss</v-btn>
          <v-btn text @click="install">Install</v-btn>
        </template>
      </v-banner>
<div class="pa-4 text-center">
        <img alt="Vue logo" src="./assets/logo.png" />
        <h1>Customize Your Vue.js PWA Installation</h1>
      </div>
    </v-app>
  </div>

</template>

<script>
console.log("Hello vue js")


export default {
  name: 'App',

  data() {
  return {
      deferredPrompt: null
    };
  },
   created() {
   console.log("created function is hitted");
    window.addEventListener("beforeinstallprompt", e => {
    console.log('beforeinstallprompt called');
      e.preventDefault();
      // Stash the event so it can be triggered later.
      this.deferredPrompt = e;
    });
window.addEventListener("appinstalled", () => {
    console.log('appinstalled called');
      this.deferredPrompt = null;
    });
  },

    methods: {
    async dismiss() {
    console.log("dismiss function is called");
      this.deferredPrompt = null;
    },
    async install() {
    console.log("install function is called");
      this.deferredPrompt.prompt();
    }
  }

};
</script>
