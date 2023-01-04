<template>

  <!--모달창-->
  <Transition name="fade">
    <ClickModal @closeModal="openModal = false" :posters="posters" :clickPoster="clickPoster" :openModal="openModal" />
  </Transition>

  <MainSlider/>

  <!--상단 고정 메뉴-->
  <div class="menu">
    <span class="siteName">My Movie Poster</span><a v-for="nav in menuName" :key="nav">{{ nav }}</a>
  </div>

  <!--메인 배너 컴포넌트-->
  <MainBanner v-if="showDiscount == true" />

  <!--정렬 버튼-->
  <div class="btnGroup">
    <button class="btn1" @click="lowPriceSort">가격낮은순</button>
    <button class="btn2" @click="highPriceSort">가격높은순</button>
    <button class="btn3" @click="sortBack">되돌리기</button>
    <button class="btn4" @click="abcSort">가나다순</button>
    <button class="btn5" @click="cbaSort">다나가순</button>
  </div>

  <!--포스터 리스트 컴포넌트-->
  <PosterList @eventModal="openModal = true; clickPoster=$event" :posterData="posters[i]"
    v-for="(posterData, i) in posters" :key="posterData" />


</template>

<script>
import posterData from './assets/data.js'; //포스터 데이터
import poster from './PosterList.vue'; //포스터 리스트 컴포넌트
import Banner from './MainBanner.vue'; //메인 배너 컴포넌트
import Modal from './ClickModal.vue'; //모달 컴포넌트


export default {
  name: 'App',
  data() {
    return {
      menuName: ['Home', 'Shop', 'About'], //상단 고정 메뉴명
      posters: posterData, //포스터 데이터
      postersOriginal: [...posterData], //포스터 데이터 유지
      showDiscount: true, //메인 배너 보여주기
      clickPoster: 0,
      openModal: false,
    }
  },
  components: {
    PosterList: poster, //포스터 리스트 컴포넌트
    MainBanner: Banner, //메인 배너 컴포넌트
    ClickModal: Modal, //모달 컴포넌트
  },
  methods: {
    //정렬 버튼 함수
    lowPriceSort() {
      this.posters.sort(function (a, b) {
        return a.price - b.price
      })
    },
    highPriceSort() {
      this.posters.sort(function (a, b) {
        return b.price - a.price
      })
    },
    abcSort() {
      this.posters.sort(function (a, b) {
        return a.title.localeCompare(b.title)
      })
    },
    cbaSort() {
      this.posters.sort(function (a, b) {
        return b.title.localeCompare(a.title)
      })
    },
    sortBack() {
      this.posters = [...this.postersOriginal];
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

body {
  margin: 0 auto;
}

div {
  box-sizing: border-box;
}

p {
  line-height: 0.5em;
}

.siteName {
  color: #d5648a;
  font-weight: 800;
  font-size: large;
  margin-right: 20px;
}

.menu {
  position: fixed;
  width: 100%;
  background-color: black;
  padding: 25px;
  text-align: left;
}

.menu a {
  color: white;
  padding: 10px;
  font-weight: 550;
  cursor: pointer;
}

.posterBox {
  float: left;
  padding: 10px;
  padding-left: 55px;
}

.posterImg {
  width: 450px;
  height: 600px;
}

.posterName {
  font-size: large;
  font-weight: 600;
}

.btnGroup {
  padding: 20px;
}

button {
  width: 90px;
  height: 30px;
  background-color: white;
  cursor: pointer;
  margin-right: -2px;
  border: 0.5px solid #8f0774;
  color: #8f0774;
  font-weight: 550;
}

button:hover {
  color: white;
  background-color: #d5648a;
}

.btn1 {
  border-top-left-radius: 5px;
  border-bottom-left-radius: 5px;
}

.btn5 {
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  margin-left: -2px;
}

.bannerImg {
  width: 95%;
  margin-top: 90px;
}

/**모달창 */
.blackBg {
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}

.whiteBg {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 30%;
  background-color: white;
  border-radius: 8px;
  padding: 20px;
}

.fade-enter-from {
  opacity: 0;
}

.fade-enter-active {
  transition: all 1s;
}

.fade-enter-to {
  opacity: 1;
}

.fade-leave-from {
  opacity: 1;
}

.fade-leave-active {
  transition: all 1s;
}

.fade-leave-to {
  opacity: 0;
}

.buy {
  margin: 10px;
}
</style>
