<template>
  <div>
    <HeaderCont />
    <section class="cont__title">
      <div class="container">
        <h1 v-for="title in titles" v-bind:key="title.text">
          {{ title.text }}
        </h1>
      </div>
    </section>
    <ContactCont />
    <FooterCont />
  </div>
</template>
<script>
import HeaderCont from "@/components/HeaderCont.vue";
// import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import FooterCont from "@/components/FooterCont.vue";
export default {
  components: {
    HeaderCont,
    // TitleCont,
    ContactCont,
    FooterCont,
  },
  data: function () {
    return {
      titles: [{ text: "reference" }, { text: "book" }],
    };
  },
};
</script>
