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
        name: "Marc",
        img: require("./assets/avatar-1.png"),
        presence: "absent",
      },
      {
        id: 1,
        name: "Ahmed",
        img: require("./assets/avatar-2.png"),
        presence: "absent",
      },
      {
        id: 2,
        name: "Bob",
        img: require("./assets/avatar-3.png"),
        presence: "absent",
      },
      {
        id: 3,
        name: "Jeanne",
        img: require("./assets/avatar-4.png"),
        presence: "absent",
      },
      // {
      //   id: 4,
      //   name: "Dalanda",
      //   img: require("./assets/Everdream.jpg"),
      //   presence: "absent",
      // },
    ],
  }),
};
</script>
