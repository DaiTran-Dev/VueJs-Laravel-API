<template>
  <div class="app flex-row align-items-center mt-5">
    <div class="container">
      <b-row class="justify-content-center login">
        <b-col md="6">
          <b-card-group>
            <b-card no-body class="p-4">
              <b-card-body>
                <h1>Register</h1>
                <Notification :message="error" v-if="error" />
                <p class="text-muted">Register account</p>
                <b-input-group class="mb-3">
                  <b-input-group-prepend>
                    <b-input-group-text
                      ><i class="icon-user"></i
                    ></b-input-group-text>
                  </b-input-group-prepend>
                  <input
                    type="text"
                    class="form-control"
                    v-model="name"
                    placeholder="name"
                  />
                </b-input-group>
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
                    <b-button variant="primary" class="px-4" @click="register"
                      >Register</b-button
                    >
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
  components: {
    Notification,
  },

  data() {
    return {
      name: "",
      email: "",
      password: "",
      error: null,
    };
  },

  methods: {
    async register() {
      try {
        await this.$axios.post("auth/register", {
          name: this.name,
          email: this.email,
          password: this.password,
        });

        await this.$auth.loginWith("local", {
          data: {
            email: this.email,
            password: this.password,
          },
        });
        this.$router.push("/");
      } catch (e) {
        this.error = e;
      }
    },
  },
};
</script>