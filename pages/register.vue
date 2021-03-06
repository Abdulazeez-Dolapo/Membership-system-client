<template>
  <v-row class="ma-0 justify-center pt-12">
    <v-col class="pa-0" cols="12" sm="9" md="6">
      <v-card class="pa-3">
        <p class="ma-0 text-h4 pb-5 black--text text-center">
          Create Account
        </p>
        <v-form ref="registerForm">
          <v-text-field
            dense
            type="text"
            primary
            label="Username"
            outlined
            :rules="usernameRules"
            v-model.trim="username"
          ></v-text-field>

          <v-text-field
            dense
            primary
            :append-icon="showText ? 'mdi-eye' : 'mdi-eye-off'"
            outlined
            :type="showText ? 'text' : 'password'"
            label="Password"
            @click:append="showText = !showText"
            :rules="passwordRules"
            v-model.trim="password"
          ></v-text-field>

          <v-row class="ma-0 justify-center align-center pb-4">
            <v-btn
              type="submit"
              depressed
              color="primary"
              block
              @click.prevent="register"
              >Sign Up</v-btn
            >
          </v-row>
        </v-form>

        <v-row class="ma-0 justify-center align-center">
          <span class="ma-0">
            Already have an account?
          </span>
          <v-spacer></v-spacer>
          <v-btn color="green" class="white--text" to="/login" depressed
            >Login</v-btn
          >
        </v-row>
      </v-card>
    </v-col>

    <notification
      @close="close"
      :dialog="notificationDialog"
      :text="notificationText"
    />
    <loading :dialog="loadingDialog" :text="loadingText" />
  </v-row>
</template>

<script>
import notification from "~/components/Notification";
import loading from "~/components/Loading";
import { handler } from "~/mixins/handler";

export default {
  layout: "authentication",
  components: {
    notification,
    loading
  },
  middleware: "auth",
  auth: "guest",
  mixins: [handler],
  data() {
    return {
      showText: false,
      timer: "",
      username: "",
      password: "",
      usernameRules: [
        v => !!v || "Username is required",
        v => v.length <= 8 || "Username must be 8 characters or less"
      ],
      passwordRules: [
        v => !!v || "Password is required",
        v => v.length >= 8 || "Password must be at least 8 characters",
        v => v.length <= 16 || "Password must be not be more than 16 characters"
      ]
    };
  },
  methods: {
    async register() {
      try {
        // Validate form inputs
        if (!this.$refs.registerForm.validate()) return;
        this.loadingText = "Creating account";
        this.loadingDialog = true;
        this.notificationDialog = false;
        this.notificationText = "";

        const payload = {
          username: this.username,
          password: this.password
        };

        let res = await this.$axios.$post("/api/auth/register", payload);

        // If succesfully signed up, login user
        if (res.success) {
          const res = await this.$auth.loginWith("local", {
            data: payload
          });

          this.loadingDialog = false;
          this.$router.push("/");
        }
      } catch (error) {
        this.handleError(error);
      }
    },
    close() {
      clearTimeout(this.timer);
      this.notificationDialog = false;
      this.notificationText = "";
    }
  }
};
</script>

<style></style>
