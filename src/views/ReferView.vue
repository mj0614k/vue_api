<template>
  <div>
    <HeaderCont />
    <TitleCont name1="reference" name2="book" />
    <section className="cont__refer">
      <div className="container">
        <div className="refer__inner">
          <h2>CSS</h2>
          <ul className="refer__list">
            <li v-for="refer in refers" :key="refer.name">
              <a href="/">
                <span className="id">{{ refer.num }}</span>
                <span className="name">{{ refer.name }}</span>
                <span className="desc">{{ refer.desc }}</span>
                <span className="descStar">{{ refer.descStar }}</span>
              </a>
            </li>
          </ul>
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
import { ref } from "vue";
import FooterCont from "@/components/FooterCont.vue";
export default {
  components: {
    HeaderCont,
    TitleCont,
    ContactCont,
    FooterCont,
  },

  setup() {
    const refers = ref([]);
    const references = () => {
      fetch("https://mj0614k.github.io/react_api/src/utils/reference.json")
        .then((response) => response.json())
        .then((result) => (refers.value = result.cssRefer))
        .catch((error) => console.log("error", error));
    };
    references();

    return {
      refers,
      references,
    };
  },
};
</script>
<style lang="scss">
.refer__inner {
  padding-bottom: 200px;
  h2 {
    font-size: 30px;
    color: var(--black);
  }
}

.refer__list {
  border: 1px solid var(--bg-light-border);
  li {
    border-bottom: 1px solid var(--bg-light-border);
    a {
      display: flex;
      width: 100%;
      color: var(--black);
      align-items: center;
      font-family: var(--font-kor);

      span {
        display: inline-block;
        padding: 15px 10px;
      }

      .num {
        flex: 1 1 5%;
        text-align: center;
        border-right: 1px solid var(--bg-light-border);
      }
      .name {
        flex: 1 1 15%;
        border-right: 1px solid var(--bg-light-border);
      }
      .desc {
        flex: 1 1 65%;
        border-right: 1px solid var(--bg-light-border);
      }
      .star {
        flex: 1 1 25%;
        text-align: center;
        border-right: 1px solid var(--bg-light-border);
      }
    }
  }
}
</style>
