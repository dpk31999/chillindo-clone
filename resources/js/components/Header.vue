<template>
  <div class="header d-md-block d-none">
    <div class="container">
      <div class="row">
          <div class="col-md-3">
            <div class="text-header">
                CHÍNH SÁCH ĐỔI TRẢ 30 NGÀY
            </div>
          </div>
          <div class="col-md-3">
            <div class="text-header">
                PHÍ GIAO HÀNG : ฿ 29
            </div>
          </div>
          <div class="col-md-3">
            <div class="text-header">
                TẤT CẢ SẢN PHẨM BẮT ĐẦU TỪ ฿ 1
            </div>
          </div>
          <div class="col-md-3">
            <div class="text-header">
                LIÊN HỆ : SUPPORT.VN@CHILINDO.COM
            </div>
          </div>
      </div>
  </div>
  </div>
</template>

<script>

    export default {

    data: () => ({
        appName: window.config.appName
    }),

    }
</script>

<style scoped>
.profile-photo {
  width: 2rem;
  height: 2rem;
  margin: -.375rem 0;
}
.header {
  background-color: #005884;
}
.text-header {
  font-size: 13px;
  color: #fff;
  text-transform: uppercase;
  text-align: left;
  line-height: 31px;
  font-style: italic;
}
</style>
