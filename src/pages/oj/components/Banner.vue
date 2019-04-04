<template>
  <div>
    <!--轮播图---写法-->
    <div class="swiper-container">
      <div class="swiper-wrapper">
        <div class="swiper-slide" v-for="item in listImg">
          <img :src="item.url">
          <!--<img src="../../assets/01.jpg"/>-->
        </div>
      </div>
      <div class="swiper-pagination swiper-pagination-white"></div>
    </div>
  </div>
</template>
<script>
import Swiper from "swiper";
import "swiper/dist/css/swiper.min.css";
export default {
  data() {
    return {
      // 图片路径
      listImg: [
        { url: "../../../../static/img/01.jpg" },
        { url: "../../../../static/img/02.jpg" },
        { url: "../../../../static/img/03.jpg" }
      ]
    };
  },
  mounted() {
    console.log("mounted", this);
    var mySwiper = new Swiper(".swiper-container", {
      loop: true,
      pagination: {
        el: ".swiper-pagination"
      },
      // 如果需要前进后退按钮
      navigation: {
        nextEl: ".swiper-button-next",
        prevEl: ".swiper-button-prev"
      },
      autoplay: {
        disableOnInteraction: false
      }
    });
  }
};
</script>
<style>
.swiper-container {
  width: 100%;
  height: auto;
}
.swiper-wrapper {
  width: 100%;
  height: 100%;
}
.swiper-slide {
  width: 100%;
  height: 100%;
}
.swiper-pagination-bullet {
  width: 0.833rem;
  height: 0.833rem;
  display: inline-block;
  background: #7c5e53;
}
.swiper-slide img {
  width: 100%;
  height: 100%;
}
</style>
