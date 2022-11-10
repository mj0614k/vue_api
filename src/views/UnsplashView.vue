<template>
  <div>
    <HeaderCont />
    <TitleCont name1="unsplash" name2="reference api" />
    <section class="cont__refer">
      <div class="container">
        <div class="unsplash__inner">
          <div class="unsplash__slider"></div>
          <div class="unsplash__search"></div>
          <div class="unsplash__images">
            <ul>
              <li v-for="splash in splashes" :key="splash.id">
                <a href="#">
                  <img :src="splash.urls.regular" :alt="splash.id" />
                </a>
              </li>
            </ul>
            <img src="" alt="" />
          </div>
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
export default {
  components: {
    HeaderCont,
    TitleCont,
    ContactCont,
    FooterCont,
  },

  setup() {
    const splashes = ref([]);
    const search = ref("landscape");

    // const SearchSplashes = () => {
    //   fetch(
    //     `https://api.unsplash.com/search/photos?client_id=CMPYww6ApEZzG93YflWFOp4WZwmnK8GSCgOgbTGxo1s&query=${search.value}`
    //   )
    //     .then((response) => response.json())
    //     .then((result) => console.log(result))
    //     .then((error) => console.log(error));
    // };
    // SearchSplashes();
    const RandomSplashes = () => {
      fetch(
        "https://api.unsplash.com/photos/random?client_id=CMPYww6ApEZzG93YflWFOp4WZwmnK8GSCgOgbTGxo1s&count=20"
      )
        .then((response) => response.json())
        .then((result) => (splashes.value = result))
        .then((error) => console.log(error));
    };
    RandomSplashes();

    return {
      splashes,
      search,
      // SearchSplashes,
      RandomSplashes,
    };
  },
};
</script>
<style lang="scss">
.unsplah__images {
  ul {
    li {
      img {
      }
    }
  }
}
</style>
