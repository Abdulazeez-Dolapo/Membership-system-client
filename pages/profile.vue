<template>
  <v-container fluid>
    <v-row class="ma-0 pl-1 justify-center justify-md-start">
      <p class="ma-0 text-h3 text-center pb-2 font-weight-bold">
        Hi {{ user.username }} !!
      </p>
    </v-row>

    <v-row class="ma-0 pl-1 justify-center justify-md-start">
      <p class="ma-0 text-h3 text-center pb-2 font-weight-bold">
        Welcome to The Members App {{ user.username }}
      </p>
    </v-row>

    <v-row class="ma-0 pl-1 justify-center justify-md-start">
      <p class="ma-0 text-h5 text-center pb-2 font-weight-bold">
        Here is your profile page
      </p>
    </v-row>

    <v-row class="ma-0 pl-1 justify-center justify-md-start">
      <p class="ma-0 text-h5 text-center pb-2 font-weight-bold">
        We hope you enjoy your stay here
      </p>
    </v-row>
  </v-container>
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
