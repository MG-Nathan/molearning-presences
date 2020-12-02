<template>
  <v-container>
    <v-row>
      <v-col v-for="student in students" :key="student.id" cols="2">
        <v-card tile elevation="4">
          <input
            type="checkbox"
            :id="student.name + student.id"
            class="d-none"
          />
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
            <TimePicker :student="student" />
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import TimePicker from "./TimePicker";

export default {
  name: "Presence",

  components: {
    TimePicker,
  },

  props: {
    students: {
      type: Array,
      required: true,
    },
  },

  data: () => ({}),

  methods: {
    validate(student) {
      if (student.presence !== "absent") {
        student.presence = "absent";
      } else {
        student.presence = "present";
      }
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
