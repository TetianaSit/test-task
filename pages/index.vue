<template>
  <section class="container">
    <img class="vector" src="../assets/images/Vector.svg" alt="">
    <header>
      <div class="logo">Logo Logo</div>
      <nav>
        <ul>
          <li>Commercial</li>
          <li>Editorial</li>
          <li>Reportage</li>
          <li>Meet me</li>
        </ul>
      </nav>
      <!--<div class="mobile-menu" v-on:click="openMenu !== openMenu">-->
        <!--<img src="../assets/images/menu.svg" alt="">-->
        <!--<div v-if="openMenu">-->
          <!--<nav>-->
            <!--<ul>-->
              <!--<li>Commercial</li>-->
              <!--<li>Editorial</li>-->
              <!--<li>Reportage</li>-->
              <!--<li>Meet me</li>-->
            <!--</ul>-->
          <!--</nav>-->
        <!--</div>-->
      <!--</div>-->
    </header>
    <main id="container">
      <transition name="fade">
        <div v-if="show === 1">
          <img class="image1" src="../assets/images/image1.png" alt="">
          <img class="image2" src="../assets/images/image2.png" alt="">
          <img class="image3" src="../assets/images/image3.png" alt="">
        </div>
      </transition>
      <transition name="fade">
        <div v-if="show === 2">
          <img class="image1" src="../assets/images/image3.png" alt="">
          <img class="image2" src="../assets/images/image1.png" alt="">
          <img class="image3" src="../assets/images/image2.png" alt="">
        </div>
      </transition>
      <transition name="fade">
        <div v-if="show === 3">
          <img class="image1" src="../assets/images/image2.png" alt="">
          <img class="image2" src="../assets/images/image3.png" alt="">
          <img class="image3" src="../assets/images/image1.png" alt="">
        </div>
      </transition>

      <div v-swiper:mySwiper="swiperOption">
        <div class="swiper-wrapper">
          <div class="swiper-slide" v-for="slide in slides" v-bind:key="slide.id">
            <div class="ink-title" v-on:mousemove="g">
              {{slide.text}}
            </div>
          </div>
        </div>
      </div>
      <div class="drag-me">Drag me</div>
    </main>
    <footer>
      <span>Inst</span>
      <div class="rect"></div>
      <span>Fb</span>
    </footer>
  </section>
</template>

<script>
import AppLogo from '~/components/AppLogo.vue'
import { TweenMax } from 'gsap'
import 'swiper/css/swiper.min.css'

export default {
  components: {
    AppLogo
  },
  data() {
    return {
      openMenu: false,
      show: 1,
      slides: [
        {
          text: 'Ink Lingerie1'
        },
        {
          text: 'Ink Lingerie2'
        },
        {
          text: 'Ink Lingerie3'
        }
      ],
      swiperOption: {
        width: 800,
        loop: true,
      }
    }
  },
  methods: {
    g() {
      if (this.mySwiper.activeIndex > this.show) {
        this.show++;
      } else if (this.mySwiper.activeIndex < this.show) {
        this.show--;
      }

      if (this.mySwiper.activeIndex > this.slides.length) {
        this.show = 1;
      } else if (this.mySwiper.activeIndex < 1) {
        this.show = this.slides.length;
      }

      if (this.show > 3) {
        this.show = 1;
      } else if (this.show < 1) {
        this.show = 1;
      }
    },
    move(e) {
      this.parallaxIt(e, ".image1", -50);
      this.parallaxIt(e, ".image2", -70);
      this.parallaxIt(e, ".image3", -100);
    },
    parallaxIt(e, target, movement) {
      let $this = document.querySelector("#container");
      let relX = e.pageX - $this.offsetLeft;
      let relY = e.pageY - $this.offsetTop;

      TweenMax.to(target, 1, {
        x: (relX - $this.offsetWidth / 2) / $this.offsetWidth * movement,
        y: (relY - $this.offsetHeight / 2) / $this.offsetHeight * movement
      });
    }
  },
  mounted() {
    window.mySwiper = this.mySwiper;
    window.addEventListener('mousemove', this.move);
  },
  destroyed() {
    window.removeEventListener('mousemove', this.move);
  }
}
</script>

<style lang="scss">

@font-face {
  font-family: Schnyder Cond XL Demi;
  src: url('../assets/fonts/Schnyder_X_Condensed/Schnyder_X_Cond_XL_Demi.otf');
}

@font-face {
  font-family: TT Travels;
  src: url('../assets/fonts/TT_Travel/TTTravels-Light.ttf');
}

.swiper-wrapper {
  width: 800px;
}

.vector {
  animation-name: example;
  animation-duration: 4s;
}

.slide {
  display: block;
  position: absolute;
  height: 200px !important;
  width: 200px !important;
  background: red;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 3s ease-in-out;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}

* {
  color: #000;
  box-sizing: border-box;
}

body {
  cursor: wait;
}

.vector {
  position: absolute;
  width: 608px;
  height: 726px;
  left: 473px;
  top: 7px;
}

header {
  width: 100%;
  height: 100px;
  display: flex;
  justify-content: space-between;
  text-align: center;
}

.logo {
  font-family: GT America;
  font-style: normal;
  font-weight: bold;
  font-size: 16px;
  line-height: 16px;
  letter-spacing: -1px;
}

ul {
  font-family: TT Travels;
  font-style: normal;
  font-weight: 300;
  font-size: 11px;
  line-height: 13px;
  text-align: right;
  letter-spacing: 0.02em;
  text-transform: capitalize;
  list-style: none;
}

main {
  height: calc(100vh - 100px);
  margin-top: -140px;
  position: relative;
  text-align: center;
  display: flex;
  align-items: center;
}

.image2 {
  position: absolute;
  display: inline-block;
  width: 238px;
  height: 331px;
  left: 229px;
  top: 201px;
  transform: rotate(1.1deg);
}

.image1 {
  position: absolute;
  width: 476px;
  height: 702px;
  left: 491px;
  top: 73px;
  transform: rotate(1.5deg);
}

.image3 {
  position: absolute;
  width: 345px;
  height: 238px;
  left: 890px;
  top: 494px;
  margin-bottom: 50px;
  margin-left: -90px;
  transform: rotate(2.03deg);
}

.drag-me {
  position: absolute;
  visibility:hidden;
  opacity: 0;
  font-family: TT Travels;
  font-size: 8px;
  line-height: 10px;
  display: flex;
  align-items: center;
  letter-spacing: 0.02em;
  right: 170px;
  top: 230px;
  text-transform: uppercase;
  transition:visibility 0.3s linear,opacity 0.3s linear;
}

div:hover + .drag-me {
  visibility:visible;
  opacity:1;
}

.ink-title {
  left: 305px;
  top: 260px;
  margin-left: 155px;
  margin-bottom: 80px;
  font-family: Schnyder Cond XL Demi;
  font-size: 140px;
  letter-spacing: 6px;
  display: flex;
  align-items: center;
  text-align: center;
  text-transform: uppercase;
  color: #580300;
  mix-blend-mode: darken;
}

.container {
  position: relative;
  height: 100vh;
  width: 100%;
  max-width: 1440px;
  padding: 40px 50px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
}

footer {
  height: 100px;
  display: flex;
  align-items: center;
}

footer > span {
  font-family: TT Travels;
  font-size: 11px;
  line-height: 13px;
  display: flex;
  align-items: flex-end;
  letter-spacing: 0.02em;
}

.rect {
  width: 56px;
  height: 1px;
  left: 81px;
  top: 808px;
  background: #393939;
  opacity: 0.24;
}

@media (max-width: 1024px) {
  .vector {
    position: absolute;
    width: 506px;
    height: 605px;
    left: 259px;
    top: 97px;
  }

  header {
    width: 100%;
    height: 100px;
    display: flex;
    justify-content: space-between;
    text-align: center;
  }

  .logo {
    position: absolute;
    width: 102px;
    height: 16px;
    left: 31px;
    top: 92px;
    font-family: GT America;
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    line-height: 16px;
    /* identical to box height, or 100% */
    letter-spacing: -1px;
  }

  ul {
    position: absolute;
    width: 75px;
    height: 88px;
    left: 917px;
    top: 97px;
    font-family: TT Travels;
    font-style: normal;
    font-weight: 300;
    font-size: 12px;
    line-height: 14px;
    text-align: right;
    letter-spacing: 0.02em;
    text-transform: capitalize;
    color: #000000;
  }

  main {
    height: calc(100vh - 100px);
    margin-top: -140px;
    position: relative;
    text-align: center;
    display: flex;
    align-items: center;
  }

  .image2 {
    position: absolute;
    width: 163px;
    height: 226px;
    left: 162.13px;
    top: 255.56px;
    transform: rotate(1.1deg);
  }

  .image1 {
    position: absolute;
    width: 359px;
    height: 530px;
    left: 339px;
    top: 147px;
    transform: rotate(1.5deg);
  }

  .image3 {
    position: absolute;
    width: 234px;
    height: 162px;
    left: 644.37px;
    top: 473.91px;
    transform: rotate(2.03deg);
  }

  .container {
    position: relative;
    height: 100vh;
    width: 100%;
    max-width: 1440px;
    padding: 40px 50px;
    margin: 0 auto;
    /*min-height: 100vh;*/
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: center;
  }

  footer {
    height: 100px;
    display: flex;
    align-items: center;
  }

  footer > span {
    font-family: TT Travels;
    font-style: normal;
    font-weight: 300;
    font-size: 12px;
    line-height: 14px;
    letter-spacing: 0.02em;
    text-transform: capitalize;
  }

  .rect {
    width: 56px;
    height: 1px;
    left: 81px;
    top: 808px;
    background: #393939;
    opacity: 0.24;
  }
}

@media (max-width: 768px) {
  .vector {
    width: 628px;
    height: 789px;
    left: 70px;
    top: 150px;
  }

  header {
    width: 100%;
    height: 100px;
    display: flex;
    justify-content: space-between;
    text-align: center;
  }

  .logo {
    font-family: GT America;
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    line-height: 16px;
    /* identical to box height, or 100% */
    letter-spacing: -1px;
  }

  ul {
    font-size: 12px;
    line-height: 14px;
  }

  main {
    height: calc(100vh - 100px);
    margin-top: -140px;
    position: relative;
    text-align: center;
    display: flex;
    align-items: center;
  }

  .image2 {
    position: absolute;
    width: 163px;
    height: 226px;
    left: 28.32px;
    top: 383.56px;
    transform: rotate(1.1deg);
  }

  .image1 {
    position: absolute;
    width: 359px;
    height: 530px;
    left: 205.19px;
    top: 275px;
    transform: rotate(1.5deg);
  }

  .image3 {
    position: absolute;
    width: 234px;
    height: 162px;
    left: 510.56px;
    top: 601.91px;
    transform: rotate(2.03deg);
  }

  /*.ink-title {*/
  /*position: absolute;*/
  /*width: 466px;*/
  /*height: 83px;*/
  /*left: 151.01px;*/
  /*top: 503px;*/
  /*font-family: Schnyder Cond XL Demi;*/
  /*font-style: normal;*/
  /*font-weight: 600;*/
  /*font-size: 96px;*/
  /*line-height: 86%;*/
  /*!* identical to box height, or 83px *!*/
  /*display: flex;*/
  /*align-items: center;*/
  /*text-align: center;*/
  /*text-transform: uppercase;*/
  /*color: #580300;*/
  /*mix-blend-mode: darken;*/
  /*}*/

  .container {
    position: relative;
    height: 100vh;
    width: 100%;
    max-width: 1440px;
    padding: 40px 50px;
    margin: 0 auto;
    /*min-height: 100vh;*/
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: center;
  }

  footer {
    height: 100px;
    display: flex;
    align-items: center;
  }

  footer > span {
    font-family: TT Travels;
    font-style: normal;
    font-weight: 300;
    font-size: 12px;
    line-height: 14px;
    letter-spacing: 0.02em;
    text-transform: capitalize;
  }

  .rect {
    width: 56px;
    height: 1px;
    left: 81px;
    top: 808px;
    background: #393939;
    opacity: 0.24;
  }
}
@media (max-width: 414px) {
  .vector {
    position: absolute;
    width: 392px;
    height: 493px;
    left: 11px;
    top: 121px;
  }

  header {
    width: 100%;
    height: 100px;
    display: flex;
    justify-content: space-between;
    text-align: center;
  }

  .logo {
    font-family: GT America;
    font-style: normal;
    font-weight: bold;
    font-size: 15px;
    line-height: 16px;
    /* identical to box height, or 107% */
    letter-spacing: -1px;
  }

  ul {
    font-family: TT Travels;
    font-style: normal;
    font-weight: 300;
    font-size: 11px;
    line-height: 13px;
    text-align: right;
    letter-spacing: 0.02em;
    text-transform: capitalize;
    list-style: none;
  }

  main {
    height: calc(100vh - 100px);
    margin-top: -140px;
    position: relative;
    text-align: center;
    display: flex;
    align-items: center;
  }

  .image1 {
    position: absolute;
    width: 273px;
    height: 403px;
    left: 76px;
    top: 163px;
    transform: rotate(1.5deg);
  }

  .image2,
  .image3  {
    display: none;
  }

  /*.ink-title {*/
  /*font-family: Schnyder Cond XL Demi;*/
  /*font-style: normal;*/
  /*font-weight: 600;*/
  /*font-size: 48px;*/
  /*line-height: 86%;*/
  /*!* identical to box height, or 41px *!*/
  /*display: flex;*/
  /*align-items: center;*/
  /*text-align: center;*/
  /*text-transform: uppercase;*/
  /*color: #580300;*/
  /*mix-blend-mode: darken;*/
  /*}*/

  .container {
    position: relative;
    height: 100vh;
    width: 100%;
    max-width: 1440px;
    padding: 40px 50px;
    margin: 0 auto;
    /*min-height: 100vh;*/
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: center;
  }

  footer {
    height: 100px;
    display: flex;
    align-items: center;
  }

  footer > span {
    font-family: TT Travels;
    font-style: normal;
    font-weight: 300;
    font-size: 12px;
    line-height: 14px;
    letter-spacing: 0.02em;
    text-transform: capitalize;
  }

  .rect {
    width: 56px;
    height: 1px;
    left: 81px;
    top: 808px;
    background: #393939;
    opacity: 0.24;
  }
}
@media (max-width: 375px) {
  .vector {
    position: absolute;
    width: 339px;
    height: 429px;
    left: 18px;
    top: 132px;
  }

  header {
    width: 100%;
    height: 100px;
    display: flex;
    justify-content: space-between;
    text-align: center;
  }

  .logo {
    font-family: GT America;
    font-style: normal;
    font-weight: bold;
    font-size: 15px;
    line-height: 16px;
    /* identical to box height, or 107% */
    letter-spacing: -1px;
  }

  ul {
    font-family: TT Travels;
    font-style: normal;
    font-weight: 300;
    font-size: 12px;
    line-height: 14px;
    text-align: right;
    letter-spacing: 0.02em;
    text-transform: capitalize;
  }

  main {
    height: calc(100vh - 100px);
    margin-top: -140px;
    position: relative;
    text-align: center;
    display: flex;
    align-items: center;
  }

  .image1 {
    position: absolute;
    width: 249.67px;
    height: 368.56px;
    left: 68.18px;
    top: 159px;
    transform: rotate(1.5deg);
  }

  /*.ink-title {*/
  /*position: absolute;*/
  /*width: 214px;*/
  /*height: 38px;*/
  /*left: 80.92px;*/
  /*top: 329.53px;*/
  /*font-family: Schnyder Cond XL Demi;*/
  /*font-style: normal;*/
  /*font-weight: 600;*/
  /*font-size: 44px;*/
  /*line-height: 86%;*/
  /*!* identical to box height, or 38px *!*/
  /*display: flex;*/
  /*align-items: center;*/
  /*text-align: center;*/
  /*text-transform: uppercase;*/
  /*}*/

  .container {
    position: relative;
    height: 100vh;
    width: 100%;
    max-width: 1440px;
    padding: 40px 50px;
    margin: 0 auto;
    /*min-height: 100vh;*/
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: center;
  }

  footer {
    height: 100px;
    display: flex;
    align-items: center;
  }

  footer > span {
    position: absolute;
    width: 214px;
    height: 38px;
    left: 80.92px;
    top: 329.53px;
  }

  .rect {
    width: 56px;
    height: 1px;
    left: 81px;
    top: 808px;
    background: #393939;
    opacity: 0.24;
  }
}
</style>

