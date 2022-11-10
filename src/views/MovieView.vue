<template>
  <div>
    <HeaderCont />
    <TitleCont name1="movie" name2="reference api" />
    <section class="cont__refer">
      <div class="container">
        <div class="movie__inner">
          <div class="movie__slider">
            <swiper
              :effect="'coverflow'"
              :grabCursor="true"
              :centeredSlides="true"
              :slidesPerView="'auto'"
              :initialSlide="2"
              :coverflowEffect="{
                rotate: 50,
                stretch: 0,
                depth: 100,
                modifier: 1,
                slideShadows: true,
              }"
              :pagination="true"
              :modules="modules"
              class="mySwiper"
            >
              <swiper-slide v-for="slider in sliders" :key="slider.id">
                <div class="item">
                  <a :href="`https://image.tmdb.org/movie/${slider.id}`">
                    <img
                      :src="`https://image.tmdb.org/t/p/w500/${slider.poster_path}`"
                      :alt="slider.title"
                    />
                  </a>
                </div>
              </swiper-slide>
            </swiper>
          </div>
          <!-- //movie__slider -->
          <div class="movie__search">
            <div className="container">
              <form @submit.prevent="SearchMovies()">
                <input
                  type="search"
                  id="search"
                  placeholder="검색어를 입력해 주세요."
                  v-model="search"
                />
                <button type="submit">검색</button>
              </form>
            </div>
          </div>
          <!-- //movie__search -->
          <div class="movie__movies">
            <div class="container">
              <ul class="movie__list">
                <li v-for="movie in movies" :key="movie.id">
                  <a :href="`https://image.tmdb.org/movie/${movie.id}`">
                    <img
                      :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
                      :alt="movie.title"
                    />
                  </a>
                </li>
              </ul>
            </div>
          </div>
          <!-- //movie__movies -->
        </div>
      </div>
    </section>
    <FooterCont />
    <ContactCont />
  </div>
</template>
<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import { ref } from "vue";

import { Swiper, SwiperSlide } from "swiper/vue";

import "swiper/css";
import "swiper/css/effect-coverflow";
import "swiper/css/pagination";

import { EffectCoverflow, Pagination } from "swiper";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
    Swiper,
    SwiperSlide,
  },
  setup() {
    const movies = ref([]);
    const sliders = ref([]);
    const search = ref("marvel");
    const SearchMovies = async () => {
      await fetch(
        `https://api.themoviedb.org/3/search/movie?api_key=62eab8f19ecf306eca5ffd98f806691d&query=${search.value}`
      )
        .then((response) => response.json())
        .then((result) => {
          console.log(result);
          movies.value = result.results;
          search.value = "";
        })
        .catch((error) => console.log(error));
    };
    SearchMovies();
    const TopMovies = async () => {
      await fetch(
        `https://api.themoviedb.org/3/movie/popular?api_key=62eab8f19ecf306eca5ffd98f806691d&`
      )
        .then((response) => response.json())
        .then((result) => (sliders.value = result.results))
        .catch((error) => console.log(error));
    };
    TopMovies();
    return {
      movies,
      sliders,
      search,
      SearchMovies,
      TopMovies,
      modules: [EffectCoverflow, Pagination],
    };
  },
};
</script>
<style lang="scss">
// container
.container {
  h2 {
    color: var(--white);
    font-size: 28px;
    margin-bottom: 10px;
  }
}

.movie__list {
  display: flex;
  flex-wrap: wrap;

  img {
    width: 100%;
    margin-bottom: 10px;
  }

  li {
    a {
      align-items: center;
      width: 100%;
      color: var(--white);
      text-align: center;

      em {
        padding: 5px 0;
        font-family: var(--font-kor);
      }

      .original_title {
        width: 100%;
        height: 67px;
        display: inline-block;
        word-break: keep-all;
        margin-bottom: 20px;
        font-size: 24px;
        font-weight: 700;
      }
      .vote_average {
        display: inline-block;
        float: right;
      }
      .title {
        display: inline-block;
        width: 100%;
        font-size: 12px;
        color: #ffffff75;
        font-family: var(--font-kor);
      }
    }
  }
}

.popular__box {
  .swiper-pagination-bullet {
    background-color: var(--white) !important;
  }
}
// moviePop__list
.moviePop__list {
  display: flex;
  flex-wrap: nowrap;
  margin-bottom: 20px;

  li {
    width: 24%;
    margin: 1%;
    position: relative;
    border: 0;
    transition: transform 0.3s;

    &:hover {
      transform: scale(1.1);
    }

    a {
      .vote_average {
        float: right;
        margin-bottom: 5px;
      }
    }
  }
}

.movie__inner {
  ul {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;

    li {
      width: 23%;
      position: relative;
      em {
        display: block;
        margin-bottom: 10px;
        font-family: var(--font-kor);
      }
      .title {
        padding: 5px 0;
        display: inline-block;
      }
      .star {
        background: #fff;
        color: black;
        position: absolute;
        left: 20px;
        top: 20px;
        width: 30px;
        height: 30px;
        border-radius: 100px;
        text-align: center;
        font-family: var(--font-main);
        line-height: 30px;
        font-weight: 800;
      }
    }
  }
  a {
    color: var(--white);
  }
}
.movie__search {
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
.swiper {
  margin-bottom: 70px;
}
.swiper-slide {
  width: 30%;
  margin-bottom: 70px;
}
.swiper-pagination-bullet-active {
  background-color: var(--black);
}
</style>
