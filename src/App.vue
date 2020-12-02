<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <Presence :students="students" />
    </v-main>
  </v-app>
</template>

<script>
import Presence from "./components/Presence";

export default {
  name: "App",

  components: {
    Presence,
  },

  data: () => ({
    students: [
      {
        id: 0,
        name: "Shannon",
        img: require("./assets/Thalia2.jpg"),
        presence: "absent",
        heureRetard: "",
      },
      {
        id: 1,
        name: "Baka",
        img: require("./assets/BlacklanceParagon.jpg"),
        presence: "absent",
      },
      {
        id: 2,
        name: "Maxime",
        img: require("./assets/seb_stasis.jpg"),
        presence: "absent",
      },
      {
        id: 3,
        name: "Nathan",
        img: require("./assets/AnsweredPrayers.jpg"),
        presence: "absent",
      },
    ],
  }),
};
</script>
