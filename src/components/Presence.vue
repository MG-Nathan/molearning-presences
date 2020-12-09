<template>
  <v-container>
    <v-row>
      <v-col v-for="student in students" :key="student.id" cols="2">
        <StudentCard :student="student" />
      </v-col>
    </v-row>
    <v-row>
      <PresenceCheck />
    </v-row>
  </v-container>
</template>

<script>
import StudentCard from "./StudentCard.vue";
import PresenceCheck from "./PresenceCheck.vue";

export default {
  name: "Presence",

  components: {
    StudentCard,
    PresenceCheck,
  },

  props: {
    students: {
      type: Array,
      required: true,
    },
  },

  data: () => ({}),

  computed: {},

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
