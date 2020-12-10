<template>
  <v-container>
    <v-tooltip right>
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          class="mx-2"
          fab
          large
          color="cyan"
          dark
          v-bind="attrs"
          v-on="on"
          @click="startMeeting"
        >
          <v-icon dark>
            mdi-video-plus
          </v-icon>
        </v-btn>
      </template>
      <span>Créer un meeting</span>
    </v-tooltip>

    <v-card class="video mt-3" v-if="meeting" elevation="5">
      <v-card-title> Nom du meeting : {{ meeting }} </v-card-title>
      <!-- EMBED JITSI MEET W/ API -->
      <div class="h100 text-center" id="meet"></div>
      <!-- EMBED JITSI MEET W/O API -->
      <!-- <div class="h100 text-center">
        <iframe
          allow="camera; microphone; fullscreen; display-capture"
          :src="'https://meet.jit.si/' + meeting"
        ></iframe>
      </div> -->

      <!-- EMBED ZOOM MEET -->
      <!-- <div class="h100 text-center">
        <iframe
          src="https://zoom.us/wc/92321555067/join?prefer=1&un=TWluZGF1Z2Fz"
          sandbox="allow-forms allow-scripts allow-same-origin"
          allow="microphone; camera"
        ></iframe>
      </div> -->
    </v-card>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    meeting: null,
    domain: "meet.jit.si",
    options: {
      roomName: this.meeting,
      parentNode: document.querySelector("#meet"),
    },
  }),
  // mounted() {
  //   let jitsiScript = document.createElement("script");
  //   jitsiScript.setAttribute("src", "https://meet.jit.si/external_api.js");
  //   document.head.appendChild(jitsiScript);
  // },
  methods: {
    startMeeting() {
      let meetingName = this.rndStr(20);
      if (this.meeting) {
        this.meeting = null;
      } else {
        this.meeting = meetingName;
      }
      const api = new JitsiMeetExternalAPI(this.domain, this.options);
      api.addEventListener("participantRoleChanged", function() {
        api.executeCommand("password", "Stronk");
      });
    },
    rndStr(len) {
      let text = "";
      let chars = "abcdefghijklmnopqrstuvwxyz-0123456789";

      for (let i = 0; i < len; i++) {
        text += chars.charAt(Math.floor(Math.random() * chars.length));
      }

      return text;
    },
  },
};
</script>

<style scoped>
.video {
  height: 75vh;
}
.h100 {
  height: 100%;
}
iframe {
  height: 90%;
  width: 99%;
  border: 0px;
}
</style>
