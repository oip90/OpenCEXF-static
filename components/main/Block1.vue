<template>
  <div class="main-top-wrapper">
    <div class="content">
      <div class="grid grid-cols-2 block1">
        <div class="block1-left">
          <h1>Start Your Way to Trade Crypto</h1>
        <!--  <p class="block-text">Trade crypto in the easiest and safest way!</p> 
          <p class="block-text">Your Way to Trade Crypto!</p> -->
          <div class="course">
            <img src="/img/btc.svg" class="inline-block" />
            <span>Price: {{ course.toFixed(2) }} USDT</span>
          </div>
        <!--  <a class="btn" href="/account/trade/BTC-USDT">Trade Bitcoin Now</a> -->
          <a class="btn" href="/account/login">Login Now</a>
        </div>
        <div class="block1-right">
          <img src="/img/top.png" class="top-image"/>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ['course']
}
</script>
<style>
.main-top-wrapper {
  background: #FFF;
  position: relative;
/* <!-- padding: 157px 0 88px; --> */
  padding: 57px 0 88px;
}
body h1 {
  color: #000;
  padding-bottom: 10px;
  font-size: 60px;
  font-weight: 700;
  line-height: 64px;
}
.block-text {
  font-size: 24px;
  color: #000;
  padding-bottom: 29px;
}
.block1-left {
  padding-top: 150px;
  color: #000;
}
.course {
  padding-bottom: 40px;
}
.course span {
  font-size: 18px;
  color: #000;
  position: relative;
  left: 2px;
  top: 1px;
}
@media(max-width: 900px) {
  .block1 {
    display: flex !important;
    flex-direction: column;
    align-items: center;
  }
  .top-image {
    position: absolute;
    top: 0;
    right: 0;
   }
  .block1-left {
    order: 1;
    padding-top: 36px;
  }
  .main-top-wrapper {
    padding: 62px 0 45px;
  }
  .block1-left h1 {
    color: #052E6B;
    padding-bottom: 12px;
    line-height: 1.4;
  }
  .block-text {
    font-size: 18px;
    color: #000;
  }
  .course span {
    font-size: 16px;
  }
  .course {
    padding-bottom: 25px;
  }
  .btn {
    height: 44px;
    font-size: 13px;
    padding: 15px 30px;
  }
}
</style>
