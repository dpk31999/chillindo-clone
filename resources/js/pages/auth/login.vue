<template>
  <div class="row">
    <div class="col-md-8 imageLogin d-flex align-items-center">
      <div class="slogan">
        <h1 class="slogan-title">Welcome Back!</h1>
        <div class="sloganAnimate">
          <h2 class="slogan-change">
            Login to access your personalised feed, and check out all the new
            products!
          </h2>
        </div>
      </div>
    </div>
    <div class="col-4 d-none d-md-block">
      <card>
        <LoginFB></LoginFB>
        <div class="line"></div>
        <div class="buttonAuth d-flex justify-content-between">
          <h2>Đăng nhập</h2>
          <h2 style="color: #b4b4b4" @click="changeAuth">Đăng kí</h2>
        </div>
        <form @submit.prevent="login" @keydown="form.onKeydown($event)">
          <div class="form-group">
            <input
              placeholder="Email"
              v-model="form.email"
              :class="{ 'is-invalid': form.errors.has('email') }"
              class="form-input"
              type="email"
              name="email"
            />
            <has-error :form="form" field="email" />
          </div>
          <div class="form-group">
            <input
              placeholder="Password"
              v-model="form.password"
              :class="{ 'is-invalid': form.errors.has('password') }"
              class="form-input"
              type="password"
              name="password"
            />
            <has-error :form="form" field="password" />
          </div>
          <div class="forgotPass" @click="toResetPassword">Quên mật khẩu</div>
          <button class="btn btn-warning rounded-lg btn-block">
            Đăng nhập
          </button>
        </form>
      </card>
    </div>
  </div>
</template>
<script>
import Form from "vform";
import LoginWithGithub from "~/components/LoginWithGithub";
import { EventBus } from "../../even-bus";
import LoginFB from "../../components/LoginWithFb";

export default {
  middleware: "guest",

  components: {
    LoginWithGithub,
    LoginFB
  },

  metaInfo() {
    return { title: this.$t("login") };
  },

  data: () => ({
    form: new Form({
      email: "",
      password: "",
    }),
    remember: false,
  }),

  methods: {
    async login() {
      // Submit the form.
      const { data } = await this.form.post("/api/login");

      // Save the token.
      this.$store.dispatch("auth/saveToken", {
        token: data.token,
        remember: this.remember,
      });

      // Fetch the user.
      await this.$store.dispatch("auth/fetchUser");

      // Redirect home.
      this.$router.push({ name: "home" });
    },

    changeAuth: function () {
      EventBus.$emit("component-a-check-status", 0);
    },

    toResetPassword: function () {
      EventBus.$emit("component-a-check-status", 2);
    },
  },
};
</script>
<style scoped>
.forgotPass {
  text-align: center;
  color: #000;
  cursor: pointer;
  margin-bottom: 17px;
}
.imageLogin {
  background: url(https://www.chilindo.com/assets/svgIcon/orangeLandingHeader.svg)
    0 50% no-repeat;
  background-size: 75%;
  height: 600px;
}
.slogan-title {
  color: #005884;
  width: 70%;
}
.sloganAnimate {
  color: #005884;
  font-weight: 800;
  margin: 90px 0;
}
.slogan-change {
  font-size: 22px;
  width: 55%;
}
.btn-login-fb {
  font-weight: 600;
  height: 45px;
}
.line {
  border-bottom: 0.5px solid black;
}
.buttonAuth h2 {
  color: #1eb7ea;
  cursor: pointer;
  font-size: 20px;
}
.buttonAuth {
  margin: 15px 0;
}
.form-input {
  width: 100%;
  background: #eaeef0;
  padding: 14px;
  box-sizing: border-box;
  border-radius: 7px;
  margin-bottom: 5px;
  border: none;
}
input:focus {
  outline: none;
}
::placeholder {
  color: red;
}
@media all and (max-width: 768px) {
  .imageLogin {
    height: 300px;
  }
  .slogan-title {
    font-size: 26px;
  }
  .sloganAnimate {
    margin: 40px 0;
  }
  .slogan-change {
    font-size: 15px;
  }
}
</style>>
  
