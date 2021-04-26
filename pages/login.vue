<template>
  <div class="app flex-row align-items-center">
    <div class="container">
      <b-row class="justify-content-center login">
        <b-col md="6">
          <b-card-group>
            <b-card no-body class="p-4">
              <b-card-body>
                <h1>Login</h1>
                <Notification :message="error" v-if="error" />
                <p class="text-muted">Sign In to your account</p>
                <b-input-group class="mb-3">
                  <b-input-group-prepend>
                    <b-input-group-text
                      ><i class="icon-user"></i
                    ></b-input-group-text>
                  </b-input-group-prepend>
                  <input
                    type="email"
                    class="form-control"
                    v-model="email"
                    placeholder="email"
                  />
                </b-input-group>

                <b-input-group class="mb-4">
                  <b-input-group-prepend>
                    <b-input-group-text
                      ><i class="icon-lock"></i
                    ></b-input-group-text>
                  </b-input-group-prepend>
                  <input
                    type="password"
                    class="form-control"
                    v-model="password"
                    placeholder="Password"
                  />
                </b-input-group>

                <b-row>
                  <b-col cols="6">
                    <b-button variant="primary" class="px-4" @click="login"
                      >Login</b-button
                    >
                  </b-col>
                  <b-col cols="12 mt-3">
                    <NuxtLink to="/register">Register</NuxtLink>
                  </b-col>
                </b-row>
              </b-card-body>
            </b-card>
          </b-card-group>
        </b-col>
      </b-row>
    </div>
  </div>
</template>

<script>
import Notification from "~/components/Notification";

export default {
  name: "Login",
  layout: "clean",
  components: {
    Notification,
  },
  data() {
    return {
      email: "devfast@gmail.com",
      password: "devfast08",
      error: null,
    };
  },
  methods: {
    async login() {
      await this.$auth.loginWith("local", {
        data: {
          email: this.email,
          password: this.password,
        },
      });
    },
  },
};
</script>