<template>
  <AuthLayout>
    <Head title="Login" />
    <div class="login-box">
      <div class="login-logo">
        <a href="https://adminlte.io/themes/v3/index2.html">TasksIn</a>
      </div>
      <div class="card">
        <div class="card-body login-card-body">
          <p class="login-box-msg">Sign up to start your session</p>
          <form @submit.prevent="form.post(route('register'))">
            
            <div class="input-group mb-3">
              <input
                id="name"
                type="name"
                class="form-control"
                :class="{ 'is-invalid': errors.name }"
                name="name"
                v-model="form.name"
                autocomplete="name"
                placeholder="Name"
              />
              <div class="input-group-append">
                <div class="input-group-text">
                  <span class="fas fa-user"></span>
                </div>
              </div>

              <span class="invalid-feedback" role="alert" v-if="errors.email">
                <strong>{{ errors.email }}</strong>
              </span>
            </div>
            <div class="input-group mb-3">
              <input
                id="email"
                type="email"
                class="form-control"
                :class="{ 'is-invalid': errors.email }"
                name="email"
                v-model="form.email"
                autocomplete="email"
                placeholder="Email"
              />
              <div class="input-group-append">
                <div class="input-group-text">
                  <span class="fas fa-envelope"></span>
                </div>
              </div>

              <span class="invalid-feedback" role="alert" v-if="errors.email">
                <strong>{{ errors.email }}</strong>
              </span>
            </div>

            <div class="input-group mb-3">
              <input
                id="password"
                type="password"
                class="form-control"
                :class="{ 'is-invalid': errors.password }"
                name="password"
                v-model="form.password"
                placeholder="Password"
              />
              <div class="input-group-append">
                <div class="input-group-text">
                  <span class="fas fa-lock"></span>
                </div>
              </div>

              <span
                class="invalid-feedback"
                role="alert"
                v-if="errors.password"
              >
                <strong>{{ errors.password }}</strong>
              </span>
            </div>

            <div class="input-group mb-3">
              <input
                id="password_confirmation"
                type="password"
                class="form-control"
                :class="{ 'is-invalid': errors.password_confirmation }"
                name="password_confirmation"
                v-model="form.password_confirmation"
                placeholder="Password_confirmation"
              />
              <div class="input-group-append">
                <div class="input-group-text">
                  <span class="fas fa-lock"></span>
                </div>
              </div>

              <span
                class="invalid-feedback"
                role="alert"
                v-if="errors.password_confirmation"
              >
                <strong>{{ errors.password_confirmation }}</strong>
              </span>
            </div>

            <div class="row">
              <div class="col-8">
                <div class="icheck-primary mt-1">
                  <a for="remember" href="#"> Forgot Password ?</a>
                </div>
              </div>

              <div class="col-4">
                <button type="submit" class="btn btn-primary btn-block">Login</button>
              </div>
            </div>

            
          </form>
        </div>
      </div>
    </div>
  </AuthLayout>
</template>

<script>
import AuthLayout from "../../layouts/back/AuthLayout.vue";
import { Head } from "@inertiajs/inertia-vue";

export default {
  components: {
    AuthLayout,
    Head,
  },
  props: {
    errors: Object,
  },
  data() {
    return {
      form: this.$inertia.form({
        name: "",
        email: "",
        password: "",
        password_confirmation: "",
      }),
    };
  },
};
</script>