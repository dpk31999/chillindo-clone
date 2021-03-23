<template>
  <div class="header">
    <div class="container">
      <div class="d-flex justify-content-between">
        <div class="logo">Chillindo</div>
        <div class="nav-authen" v-if="authenticated">
          <a href="#" class="dropdown-item pl-3" @click.prevent="logout">
            <fa icon="sign-out-alt" fixed-width />
            {{ $t("logout") }}
          </a>
        </div>
        <div class="nav-normal" v-else>
          <div class="d-md-block d-none">
            <div @click="changeAuth" class="text-sign">
              <template v-if="isLogin"> Sign Up Here </template>
              <template v-else> Already a Customer? Login Here </template>
            </div>
          </div>
          <div class="d-md-none d-block d-flex">
            <div class="text-sign mr-3">Đăng ký</div>
            <div class="text-sign">Đăng nhập</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import LocaleDropdown from "./LocaleDropdown";
import { EventBus } from "../even-bus";

export default {
  components: {
    LocaleDropdown,
  },

  data: () => ({
    appName: window.config.appName,
    isLogin: false,
  }),

  computed: mapGetters({
    user: "auth/user",
    authenticated: "auth/check",
  }),

  methods: {
    async logout() {
      // Log out the user.
      await this.$store.dispatch("auth/logout");

      // Redirect to login.
      this.$router.push({ name: "home" });
    },

    changeAuth: function () {
      this.isLogin = !this.isLogin;

      EventBus.$emit("component-a-check-status", this.isLogin ? 1 : 0);
    },
  },
};
</script>

<style scoped>
.profile-photo {
  width: 2rem;
  height: 2rem;
  margin: -0.375rem 0;
}
.header {
  background-color: #1ab7ea;
  padding: 15px 0 14px;
  z-index: 10;
  display: block;
  position: sticky;
  top: 0;
  transition: all 0.25s ease-in-out;
  box-shadow: 0 0 5px 0 rgb(0 0 0 / 22%);
}
.logo {
  font-size: 20px;
  color: #fff;
  font-style: italic;
  font-weight: bold;
}
.text-sign {
  font-size: 15px;
  color: #fff;
  cursor: pointer;
}
</style>
