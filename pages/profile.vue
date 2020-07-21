<template>
  <div>
    <v-row class="ma-0 pl-1 justify-center justify-md-start">
      <p class="ma-0 text-h3 pb-2 font-weight-bold">
        Welcome to The Members App {{ user.username }}
      </p>
    </v-row>

    <v-row class="ma-0 pl-1 justify-center justify-md-start">
      <p class="ma-0 text-h5 pb-2 font-weight-bold">
        We hope you enjoy your stay here
      </p>
    </v-row>
  </div>
</template>

<script>
export default {
  middleware: "auth",
  data() {
    return {
      user: this.$auth.$state.user
    };
  }
};
</script>
