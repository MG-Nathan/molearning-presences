<template>
  <v-dialog v-model="dialog" persistent max-width="290">
    <template v-slot:activator="{ on, attrs }">
      <v-btn color="primary" dark v-bind="attrs" v-on="on" @click="timer">
        Vérifier les présences
      </v-btn>
    </template>
    <v-card :style="position">
      <!-- <template slot="progress">:loading="loading" 
        <v-progress-linear height="5" :value="loadState"></v-progress-linear>
      </template> -->
      <v-card-title class="headline">
        Élève, es-tu là ?
      </v-card-title>
      <v-card-text class="text-center">
        <v-avatar color="success">
          <span class="white--text headline">{{ loadState }}</span>
        </v-avatar>
      </v-card-text>
      <v-card-actions>
        <v-btn color="green darken-1" text @click="validate()">
          Oui !
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: "PresenceCheck",

  data: () => ({
    dialog: false,
    // loading: false,
    loadState: 0,
    time: 5000, //temps d'affichage du modal en millisecondes
    position: null,
    timeout: null,
    interval: null,
    présence: "absent",
  }),

  computed: {
    start() {
      return this.time / 1000;
    },
  },

  methods: {
    timer() {
      this.position = {
        position: "absolute",
        left: Math.floor(Math.random() * (80 - 20) + 20) + "%",
        top: Math.floor(Math.random() * (80 - 20) + 20) + "%",
        width: "auto",
      };
      // this.loading = true;
      this.loadState = Math.floor(this.time / 1000);

      this.interval = setInterval(() => {
        this.loadState--;
      }, 1000);

      this.timeout = setTimeout(() => {
        if (this.dialog !== false) {
          // this.loading = false;
          (this.présence = "absent"), (this.dialog = false);
        }
        clearInterval(this.interval);
      }, this.time);
    },
    validate() {
      // this.loading = false;
      (this.présence = "présent"), (this.dialog = false);
      clearTimeout(this.timeout);
      clearInterval(this.interval);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
