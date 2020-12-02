<template>
  <v-card tile elevation="4">
    <input type="checkbox" :id="student.name + student.id" class="d-none" />
    <label :for="student.name + student.id" @click="validate(student)">
      <v-img :src="student.img" class="white--text align-end">
        <v-system-bar
          height="32"
          absolute
          :color="
            student.presence === 'present'
              ? 'success'
              : student.presence === 'late'
              ? 'warning'
              : 'red'
          "
          class="faded"
        >
          <v-spacer></v-spacer>
          <v-icon>{{
            student.presence === "present"
              ? "mdi-checkbox-marked-circle"
              : student.presence === "late"
              ? "mdi-clock-alert"
              : "mdi-cancel"
          }}</v-icon>
          <span>{{
            student.presence === "present"
              ? "Présent(e)"
              : student.presence === "late"
              ? "En retard (" + student.heureRetard + ")"
              : "Absent(e)"
          }}</span>
        </v-system-bar>
        <v-card-title v-text="student.name"></v-card-title>
      </v-img>
    </label>
    <v-card-actions v-if="student.presence === 'absent'">
      <!-- Time Picker -->
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
            prepend-icon="mdi-clock-time-four-outline"
            @click:prepend="getNow"
            append-icon="mdi-eraser"
            @click:append="clear"
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
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "StudentCard",

  props: {
    student: {
      type: Object,
      required: true,
    },
  },

  data: () => ({
    time: null,
    menu: false,
  }),

  methods: {
    validate(student) {
      if (student.presence !== "absent") {
        student.presence = "absent";
      } else if (this.time !== null) {
        student.presence = "late";
        student.heureRetard = this.time;
      } else {
        student.presence = "present";
      }
    },
    clear() {
      this.time = null;
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.faded {
  opacity: 75%;
}
</style>
