<template>
  <v-card :style="randomPos()">
    <v-card-title class="headline">
      Êtes-vous présent ?
    </v-card-title>
    <v-card-text class="text-center">
      <!-- <Timer :time="time" /> -->
      <v-avatar color="success">
        <!-- <span class="white--text headline">{{ this.loadState }}</span> -->
      </v-avatar>
    </v-card-text>
    <v-card-actions>
      <v-btn color="green darken-1" text @click="emitClick">
        Oui !
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  computed: {},
  methods: {
    randomPos() {
      return {
        position: "absolute",
        left: Math.floor(Math.random() * (80 - 20) + 20) + "%",
        top: Math.floor(Math.random() * (80 - 20) + 20) + "%",
        width: "auto",
      };
    },
    emitClick() {
      this.$emit("clicked");
    },
  },
};
</script>

<style></style>
