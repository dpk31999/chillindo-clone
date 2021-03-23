<template>
    <div>
        <template v-if="numberCheckState == 1">
            <Login></Login>
        </template>
        <template v-if="numberCheckState == 0">
            <Register></Register>
        </template>
        <template v-if="numberCheckState == 2">
            <ResetPassword></ResetPassword>
        </template>
    </div>
</template>
<script>
import {mapGetters} from 'vuex'
import { EventBus } from '../even-bus'
import Login from '../pages/auth/login'
import Register from '../pages/auth/register'
import ResetPassword from '../pages/auth/password/email'

export default {
  middleware: "guest",

  metaInfo(){
    return {title : "Home"}
  },
  data: () => ({
    numberCheckState : 0 // if it equal 0 then to register, 1 to login and 2 to reset password
  }),
  computed : mapGetters({
    authenticated : 'auth/check'
  }),
  components : {
    Login,
    Register,
    ResetPassword
  },
  mounted() {
    EventBus.$on('component-a-check-status', number => {
      this.numberCheckState = number
    });

  }
}
</script>
<style scoped>

</style>