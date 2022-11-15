<template>
  <div>
    <HeaderCont />
    <TitleCont name1="youtube" name2="reference api" />
    <section class="cont__refer">
      <div class="container">
        <div class="youtube__inner">
          <h2>POPULAR Videos</h2>
          <div class="youtube__popular">
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
                  <a
                    :href="`https://www.youtube.com/watch?v=${slider.id.videoId}`"
                  >
                    <img :src="`${slider.snippet.thumbnails.medium.url}`" />
                    <span class="title">{{ slider.snippet.title }}</span>
                  </a>
                </div>
              </swiper-slide>
            </swiper>
          </div>
          <!-- //youtube__slider -->
          <div class="youtube__search">
            <form @submit.prevent="SearchYoutubes()">
              <input
                type="search"
                id="search"
                placeholder="검색어를 입력해 주세요."
                v-model="search"
              />
              <button type="submit">검색</button>
            </form>
          </div>
          <!-- //youtube__search -->
          <div className="youtube__tag">
            <button type="submit" onClick="{onClick1}">html</button>
            <button type="submit" onClick="{onClick2}">css</button>
            <button type="submit" onClick="{onClick3}">javascript</button>
            <button type="submit" onClick="{onClick4}">react</button>
            <button type="submit" onClick="{onClick5}">vue</button>
            <button type="submit" onClick="{onClick6}">web</button>
          </div>
          <!-- //youtube__tag -->
          <div class="youtube__youtubes">
            <ul class="youtube__list">
              <li v-for="vedio in vedios" :key="vedio.id">
                <a
                  :href="`https://www.youtube.com/watch?v=${vedio.id.videoId}`"
                >
                  <img :src="`${vedio.snippet.thumbnails.medium.url}`" />
                  <p class="title">{{ vedio.snippet.title }}</p>
                </a>
              </li>
            </ul>
          </div>
          <!-- //youtube__youtubes -->
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
    const vedios = ref([]);
    const sliders = ref([]);
    const search = ref("html");
    const SearchYoutubes = async () => {
      await fetch(
        `https://youtube.googleapis.com/youtube/v3/search?key=AIzaSyDScK_kd_EDAf9lp5tqhRjnyc1f34kDTrE&part=snippet&q=${search.value}&maxResults=30&type=video`
      )
        .then((response) => response.json())
        .then((result) => {
          vedios.value = result.items;
          search.value = "";
        })
        .catch((error) => console.log(error));
    };
    SearchYoutubes();
    const TopYoutubes = async () => {
      await fetch(
        `https://youtube.googleapis.com/youtube/v3/videos?part=snippet&chart=mostPopular&maxResults=10&key=AIzaSyDScK_kd_EDAf9lp5tqhRjnyc1f34kDTrE`
      )
        .then((response) => response.json())
        .then((result) => (sliders.value = result.items))
        .catch((error) => console.log(error));
    };
    TopYoutubes();
    return {
      vedios,
      sliders,
      search,
      SearchYoutubes,
      TopYoutubes,
      modules: [Pagination],
    };
  },
};
</script>
<style lang="scss">
.youtube__popular {
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
    }
  }
  .youtube__slider {
    .swiper-pagination-bullet {
      background-color: var(--black);
    }
  }
  em {
    display: block;
    margin-bottom: 10px;
    font-family: var(--font-kor);
  }
  .title {
    padding: 5px 0;
    display: inline-block;
    width: 100%;
    text-align: center;
    color: var(--black);
    font-weight: 500;
    font-family: var(--font-kor);
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
}
.youtube__inner {
  h2 {
    color: var(--black);
    font-size: 28px;
    margin-bottom: 30px;
  }
}
.youtube__search {
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
.youtube__tag {
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
.youtube__list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  li {
    width: 32%;
    margin-bottom: 30px;
    transition: all 0.3s;
    &:hover {
      transform: scale(1.1);
    }
    em {
      display: block;
      margin-bottom: 10px;
      font-family: var(--font-kor);
    }
    .title {
      padding: 5px 0;
      text-align: left;
      display: inline-block;
      width: 100%;
      text-align: left;
      color: var(--black);
      font-weight: 500;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      font-family: var(--font-kor);
    }
  }
}
</style>
