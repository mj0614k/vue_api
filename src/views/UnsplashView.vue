<template>
  <div>
    <HeaderCont />
    <TitleCont name1="unsplash" name2="reference api" />
    <section class="cont__unsplash">
      <div class="container">
        <div class="unsplash__inner">
          <h2>RANDOM IMAGE</h2>
          <div class="unsplash__slider">
            <swiper
              :slidesPerView="'auto'"
              :centeredSlides="true"
              :spaceBetween="30"
              :pagination="{
                clickable: true,
              }"
              :modules="modules"
              class="mySwiper"
              :initialSlide="1"
            >
              <swiper-slide v-for="(slider, index) in sliders" :key="index">
                <div class="item">
                  <a :href="`...`">
                    <figure class="unsplash__image">
                      <img :src="slider.urls.regular" :alt="slider.id" />
                    </figure>
                  </a>
                </div>
              </swiper-slide>
            </swiper>
          </div>
          <div class="unsplash__search">
            <form @submit.prevent="SearchYoutubes()">
              <input type="search" id="search" placeholder="검색어를 입력해 주세요." v-model="search" />
              <button type="submit">검색</button>
            </form>
          </div>
          <!-- //unsplash__search -->
          <div className="unsplash__tag">
            <button type="submit" onClick="{onClick1}">dog</button>
            <button type="submit" onClick="{onClick2}">cat</button>
            <button type="submit" onClick="{onClick3}">alpaca</button>
            <button type="submit" onClick="{onClick4}">hamster</button>
            <button type="submit" onClick="{onClick5}">bear</button>
            <button type="submit" onClick="{onClick6}">elephant</button>
            <button type="submit" onClick="{onClick7}">rabbit</button>
          </div>
          <div class="unsplash__images">
            <ul class="unsplash__list">
              <li v-for="(splash, index) in splashes" :key="index">
                <a :href="`...`">
                  <img :src="splash.urls.regular" :alt="splash.id" />
                </a>
              </li>
            </ul>
          </div>
          <!-- //unsplash__images -->
        </div>
      </div>
    </section>
    <ContactCont />
    <FooterCont />
  </div>
</template>
<script>
import HeaderCont from "@/components/HeaderCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import { ref } from "vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";
import "swiper/css/pagination";

import { Pagination } from "swiper";
export default {
  components: {
    HeaderCont,
    TitleCont,
    ContactCont,
    FooterCont,
    Swiper,
    SwiperSlide,
  },

  setup() {
    const splashes = ref([]);
    const sliders = ref([]);
    const search = ref("dog");

    const SearchSplashes = async () => {
      await fetch(`https://api.unsplash.com/search/photos?client_id=CMPYww6ApEZzG93YflWFOp4WZwmnK8GSCgOgbTGxo1s&query=${search.value}`)
        .then((response) => response.json())
        .then((result) => {
          splashes.value = result;
          search.value = "";
        })
        .catch((error) => console.log(error));
    };
    SearchSplashes();
    const RandomSplashes = async () => {
      await fetch("https://api.unsplash.com/photos/random?client_id=CMPYww6ApEZzG93YflWFOp4WZwmnK8GSCgOgbTGxo1s&count=20")
        .then((response) => response.json())
        .then((result) => (sliders.value = result))
        .catch((error) => console.log(error));
    };
    RandomSplashes();

    return {
      splashes,
      sliders,
      search,
      SearchSplashes,
      RandomSplashes,
      modules: [Pagination],
    };
  },
};
</script>
<style lang="scss">
.cont__unsplash {
  ul {
    column-count: 4;
    column-gap: 20px;
    width: 100%;

    li {
      margin-bottom: 20px;
      transition: all 0.3s;

      &:hover {
        transform: scale(1.1);
      }
    }
  }
}
.unsplash__inner {
  h2 {
    color: var(--black);
    font-size: 28px;
    margin-bottom: 30px;
  }
  .swiper {
    margin-bottom: 90px;
  }
  .swiper-slide {
    width: 30%;
    margin-bottom: 70px;
    .item {
      transition: all 0.3s;
      &:hover {
        transform: scale(1.1);
      }
      .unsplash__image {
        width: 400px;
        height: 400px;
        overflow: hidden;
        position: relative;
        img {
          width: 80%;
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
        }
      }
    }
  }
  .unsplash__slider {
    .swiper-pagination-bullet {
      background-color: var(--black);
    }
  }
}
.unsplash__search {
  margin-bottom: 100px;

  .container {
    position: relative;
  }

  h2 {
    color: var(--white);
    font-size: 40px;
    text-indent: -9999px;
    height: 0;
  }
  input {
    background: var(--white);
    border: 2px solid var(--white);
    border-radius: 50px;
    color: var(--black);
    width: 100%;
    padding: 15px 100px 15px 30px;
    font-family: var(--font-kor);
  }
  button {
    background-color: var(--black);
    color: var(--white);
    position: absolute;
    right: 10px;
    top: 8px;
    width: 80px;
    height: 40px;
    border-radius: 50px;
    border: 0;
    font-family: var(--font-kor);
    cursor: pointer;
    z-index: 1000;
  }
}
.unsplash__tag {
  margin-bottom: 100px;

  button {
    padding: 10px 20px;
    border-radius: 10px;
    background-color: #fff;
    margin-right: 10px;
    color: var(--black);
    font-family: var(--font-kor);
    border: 0;
    cursor: pointer;
    z-index: 10;
    transition: all 0.3s;
    &:hover {
      background-color: rgba(255, 255, 255, 0.2);
    }
  }
}
</style>
