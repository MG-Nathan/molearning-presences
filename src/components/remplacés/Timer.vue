<template>
  <v-avatar color="success">
    <span class="white--text headline">{{ this.loadState }}</span>
  </v-avatar>
</template>

<script>
export default {
  name: "Timer",

  props: {
    time: {
      type: Number,
      required: true,
    },
    start: {
      type: Number,
      required: true,
    },
  },

  data: () => ({
    loadState: 0,
  }),

  methods: {
    countdown() {
      this.loadState = this.start;
      let timer = setInterval(() => {
        console.log(this.loadState);

        this.loadState--;
      }, 1000);

      setTimeout(() => {
        clearInterval(timer);
        this.$emit("end");
      }, this.time);
    },
  },

  mounted() {
    this.countdown();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
