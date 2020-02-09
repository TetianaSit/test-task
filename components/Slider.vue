<template>
  <section>
    <div>hgcmh</div>
    <div v-swiper:mySwiper>
      <div class="swiper-wrapper">
        <div class="swiper-slide">
          Ink Lingerie
        </div>
        <div class="swiper-slide">
          Ink Lingerie
        </div>
        <div class="swiper-slide">
          Ink Lingerie
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import 'swiper/css/swiper.min.css'
export default {
  data() {
    return {
      swiperOption: {
        // some swiper options...
      }
    }
  },
  mounted() {
    // setTimeout(() => {
    //   this.banners.push('/_nuxt/assets/images/image3.png')
    //   console.log('banners update')
    // }, 3000)
    console.log(
      'This is current swiper instance object', this.mySwiper,
      'It will slideTo banners 3')
    // this.mySwiper.slideTo(3, 1000, false)
  }
}
</script>

<style>
.swiper-container img {
  width: 400px;
}
.swiper-container {
  width: 400px;
}

</style>

