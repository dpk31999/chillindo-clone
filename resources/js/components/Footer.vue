<template>
  <div class="footer">
    <div class="container">
      <div class="row footer-info pt-5 pb-5">
        <div class="col-md-7">
          <div class="row">
            <div class="col-6 text-left">
              <h4 class="title-footer pb-3">Trợ giúp & Liên Hệ</h4>
              <p>Contact</p>
              <p>Delivery Info</p>
              <p>Registration</p>
              <p>Building Help</p>
              <p>Payment & Shipping</p>
            </div>
            <div class="col-6 text-left">
              <h4 class="title-footer pb-3">Về Chilindo</h4>
              <p>About Us</p>
              <p>User Agreement</p>
              <p>Privacy Policy</p>
              <p>Company Info</p>
            </div>
          </div>
        </div>
        <div class="col-md-5">
          <div class="d-flex flex-column bd-highlight contact">
            <div class="contact-top text-sm-left text-center">
              <h4 class="title-footer pb-3">Connect with us</h4>
              <div class="icon-contact d-flex">
              </div>
            </div>
            <div class="contact-bottom text-sm-right text-center">
              <p>Có câu hỏi? Chúng tôi muốn nghe từ bạn!</p>
              <p>Email cho chúng tôi: support@chilindo.com</p>
            </div>
          </div>
        </div>
      </div>
      <div class="line"></div>
      <div class="footer-copyright text-center p-4">
        COPYRIGHT @ 2019 CHILINDO.COM. ALL RIGHTS RESERVED.
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    appName: window.config.appName,
  }),
};
</script>

<style scoped>
.profile-photo {
  width: 2rem;
  height: 2rem;
  margin: -0.375rem 0;
}
.footer {
  background-color: #18b7ea;
  color: #fff;
}
.line {
  border: 0.1px solid #fff;
}
.title-footer {
  font-size: 20px;
  font-weight: 600;
}
.footer-copyright {
  font-weight: bold;
}

/* .contact-top {
  position: absolute;
  top: 0%;
  left: 0%;
}
.contact-bottom {
  position: absolute;
  right: 0%;
  bottom: 0%;
} */
</style>
