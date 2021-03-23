<template>
  <div class="row">
    <div class="col-md-8 imageRegister d-flex align-items-center">
      <div class="slogan">
        <h1 class="slogan-title">Thousands of Auctions starting at 1 THB</h1>
        <div class="sloganAnimate">
          <h2 class="slogan-change">We Auction CLOTHES</h2>
        </div>
      </div>
    </div>
    <div class="col-4 d-none d-md-block">
      <card>
        <LoginFB></LoginFB>
        <div class="line"></div>
        <div class="buttonAuth d-flex justify-content-between">
          <h2>Đăng kí</h2>
          <h2 style="color : #b4b4b4;" @click="changeAuth">Đăng nhập</h2>
        </div>
        <form @submit.prevent="register" @keydown="form.onKeydown($event)">
          <div class="form-group">
            <input v-model="form.username" placeholder="Tên tài khoản *" :class="{ 'is-invalid': form.errors.has('username') }" class="form-input" type="text" name="username">
            <has-error :form="form" field="username" />
          </div>
          <div class="form-group">
            <input v-model="form.email" placeholder="Email *" :class="{ 'is-invalid': form.errors.has('email') }" class="form-input" type="email" name="email">
            <has-error :form="form" field="email" />
          </div>
          <div class="form-group">
            <input v-model="form.password" placeholder="Mật khẩu *" :class="{ 'is-invalid': form.errors.has('password') }" class="form-input" type="password" name="password">
            <has-error :form="form" field="password" />
          </div>
          <div class="form-group">
            <input v-model="form.password_confirmation" placeholder="Xác nhận mật khẩu *" :class="{ 'is-invalid': form.errors.has('password_confirmation') }" class="form-input" type="password" name="password_confirmation">
            <has-error :form="form" field="password_confirmation" />
          </div>
          <div class="terms text-center">
             <div>By clicking Sign Up, you agree to the </div>
            <span>
              <a href="">Terms & Conditions</a>
              and
              <a href="">Privacy Policy</a>
            </span>
          </div>
          <button class="btn btn-warning rounded-lg btn-block">BẮT ĐẦU ĐẤU GIÁ</button>
        </form>
      </card>
    </div>
  </div>
</template>

<script>
import Form from 'vform'
import { EventBus } from '../../even-bus';
import LoginFB from "../../components/LoginWithFb";

export default {
  middleware: 'guest',

  components: {
    LoginFB
  },

  metaInfo () {
    return { title: this.$t('register') }
  },

  data: () => ({
    form: new Form({
      username: '',
      email: '',
      password: '',
      password_confirmation: ''
    }),
    mustVerifyEmail: false
  }),

  methods: {
    async register () {
      // Register the user.
      const { data } = await this.form.post('/api/register')

      // Must verify email fist.
      if (data.status) {
        this.mustVerifyEmail = true
      } else {
        // Log in the user.
        const { data: { token } } = await this.form.post('/api/login')

        // Save the token.
        this.$store.dispatch('auth/saveToken', { token })

        // Update the user.
        await this.$store.dispatch('auth/updateUser', { user: data })

        // Redirect home.
        this.$router.push({ name: 'home' })
      }
    },

    changeAuth : function() {
      EventBus.$emit('component-a-check-status', 1);
    }
  }
}
</script>
<style scoped>
.imageRegister {
  background: url(https://www.chilindo.com/assets/svgIcon/blueLandingHeader.svg) 0 50% no-repeat;
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
.terms {
  color: #ff9999;
  font-size: 11px;
  margin-bottom: 17px;
  height: 30px;
}

@media all and (max-width: 768px) {
   .imageRegister {
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
</style>
