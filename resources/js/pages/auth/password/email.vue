<template>
  <div class="row">
    <div class="col-md-8 imageLogin d-flex align-items-center">
      <div class="slogan">
        <h1 class="slogan-title">Welcome Back!</h1>
        <div class="sloganAnimate">
          <h2 class="slogan-change">Login to access your personalised feed, and check out all the new products!</h2>
        </div>
      </div>
    </div>
    <div class="col-4 d-none d-md-block">
      <card>
        <LoginFB></LoginFB>
        <div class="line"></div>
        <div class="pt-4 pb-5">
          <h3>Quên mật khẩu</h3>
          <p>Please enter your registered Email to receive password reset instructions.</p>
        </div>
        <form @submit.prevent="send" @keydown="form.onKeydown($event)">
          <div class="form-group">
            <input v-model="form.email" placeholder="Email" :class="{ 'is-invalid': form.errors.has('email') }" class="form-input" type="email" name="email">
              <has-error :form="form" field="email" />
          </div>
          <p v-if="sended" class="text-success">Nếu địa chỉ email bạn nhập đã tồn tại, bạn sẽ nhận được một email hướng dẫn đặt lại mật khẩu</p>
          <v-button :loading="form.busy" class="btn btn-info rounded-lg btn-block font-weight-bold">
            ĐẶT LẠI MẬT KHẨU
          </v-button>
        </form>
        <div class="text-center p-2 text-info" style="cursor: pointer;" @click="toLogin">Đăng nhập</div>
      </card>
    </div>
  </div>
</template>

<script>
import { EventBus } from '../../../even-bus';
import Form from 'vform'
import LoginFB from "../../../components/LoginWithFb";


export default {
  middleware: 'guest',

  components: {
    LoginFB
  },

  metaInfo () {
    return { title: this.$t('reset_password') }
  },

  data: () => ({
    status: '',
    form: new Form({
      email: ''
    }),
    sended : false
  }),

  methods: {
    async send () {
      const { data } = await this.form.post('/api/password/email')

      this.status = data.status

      this.form.reset()

      this.sended = true
    },
    toLogin : function () {
      EventBus.$emit('component-a-check-status', 1);
    }
  }
}
</script>
<style scoped>
.imageLogin {
  background: url(https://www.chilindo.com/assets/svgIcon/orangeLandingHeader.svg) 0 50% no-repeat;
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
</style>