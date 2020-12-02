<template>
  <v-menu
    ref="menu"
    v-model="menu"
    :close-on-content-click="false"
    :nudge-right="40"
    :return-value.sync="time"
    transition="scale-transition"
    offset-y
    max-width="290px"
    min-width="290px"
  >
    <template v-slot:activator="{ on, attrs }">
      <v-text-field
        v-model="time"
        label="Retard"
        hint="Heure d'arrivée"
        :rules="rules"
        prepend-icon="mdi-clock-time-four-outline"
        @click:prepend="getNow"
        append-icon="mdi-content-save"
        @click:append="saveLate(student)"
        readonly
        v-bind="attrs"
        v-on="on"
        @change="saveTime"
      ></v-text-field>
    </template>

    <v-time-picker
      v-if="menu"
      v-model="time"
      format="24hr"
      scrollable
      full-width
      @click:minute="$refs.menu.save(time)"
    ></v-time-picker>
  </v-menu>
</template>

<script>
export default {
  name: "TimePicker",

  props: {
    student: {
      type: Object,
      required: true,
    },
  },

  data: () => ({
    time: null,
    menu: false,
    rules: [(value) => !!value || "Veuillez choisir une heure."],
  }),

  methods: {
    saveLate(student) {
      if (this.time !== null) {
        student.presence = "late";
        student.heureRetard = this.time;
      }
    },
    saveTime() {
      this.$emit("changed", this.time);
    },
    getNow() {
      const today = new Date();
      const time =
        (today.getHours() < 10 ? "0" : "") +
        today.getHours() +
        ":" +
        (today.getMinutes() < 10 ? "0" : "") +
        today.getMinutes();
      this.time = time;
    },
  },
};
</script>
