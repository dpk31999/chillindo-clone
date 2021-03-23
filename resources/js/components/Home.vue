<template>
    <div>
        Home
    </div>
</template>
<script>
import {mapGetters} from 'vuex'

export default {
  middleware: 'auth',
  
  metaInfo(){
    return {title : "Home"}
  },
  computed : mapGetters({
    authenticated : 'auth/check'
  }),
}
</script>