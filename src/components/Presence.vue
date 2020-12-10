<template>
  <v-container>
    <v-tabs v-model="tab">
      <v-tab key="presences"> Présences </v-tab>
      <v-tab key="video"> Video Call </v-tab>
    </v-tabs>
    <v-tabs-items v-model="tab">
      <v-tab-item key="presences">
        <v-row>
          <v-col v-for="student in students" :key="student.id" cols="2">
            <StudentCard :student="student" />
          </v-col>
        </v-row>
        <v-row> <PresenceCheck /> </v-row>
      </v-tab-item>
      <v-tab-item key="video">
        <Jitsi />
      </v-tab-item>
    </v-tabs-items>
  </v-container>
</template>

<script>
import StudentCard from "./StudentCard.vue";
import PresenceCheck from "./PresenceCheck.vue";
import Jitsi from "./Jitsi";

export default {
  name: "Presence",

  components: {
    StudentCard,
    PresenceCheck,
    Jitsi,
  },

  props: {
    students: {
      type: Array,
      required: true,
    },
  },

  data: () => ({
    tab: null,
  }),

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
