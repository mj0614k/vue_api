<template>
  <div>
    <HeaderCont />
    <TitleCont name1="about" name2="ME" />
    <section className="cont__about">
      <div className="container">
        <div className="cont__inner">
          <div className="cont__about1">
            <img
              src="https://github.com/mj0614k/react_api/blob/main/src/assets/img/aboutImg01.jpg?raw=true"
              alt="이미지1"
            />
            <h2>꿈을 설계하고 디자인하다.</h2>
            <p>
              나는 공간을 만드는 것을 좋아한다. 어렸을 때부터 나만의 공간을
              만드는 것을 좋아했고, 나만의 다락방을 좋아했다. 단 한 사람이라도
              내가 만든 공간 속에서 영감을 받거나 마음이 움직였으면 좋겠다.
              서울에는 집이 없지만, 이곳에서는 나만의 집이 많다. 그 집은 비용도
              들지 않고 언제든지 만들 수 있다. 나만의 공간을 마음껏 만들 수
              있다는 건 코딩의 엄청난 매력인 것 같다. 앞으로도 그 한 구석에
              나만의 꿈을 설계하고 디자인을 하며 살고 싶다.
            </p>
          </div>
          <div className="cont__about2">
            <img
              src="https://github.com/mj0614k/react_api/blob/main/src/assets/img/aboutImg02.jpg?raw=true"
              alt="이미지2"
            />
            <div className="cont__layout">
              <h2>열심히 할수록 기회는 따른다.</h2>
              <p>
                운이 좋은 사람은 없다. 단지 운을 만들 뿐이다. 운을 만들기
                위해서는 내가 좋아하는 일이나 내가 하고 싶은 일에 몰두하면 된다.
                몰두하다 보면 길이 보이고 방향이 보이게 된다. 운이란 고된 노동과
                노력을 통해 스스로 만들어 내는 것이다. 복권에 당첨되는 사람들은
                금방 돈을 허비하게 된다. 단지 운만 좋았기 때문이다. 운을 만든
                사람은 돈을 날려먹거나 헛되게 쓰지 않는다. 열심히 할수록 운은
                나에게 온다.
              </p>
            </div>
          </div>
          <div className="cont__about3">
            <div className="cont__layout">
              <h2>나에게 정직하다.</h2>
              <p>
                정직은 다른 사람보다 나에게 큰 의미를 부여해야 한다. 자신이
                정직하지 않으면 진정으로 원하는 일을 열정적으로 밀고 나갈 수
                없다. 마음에서 우러나오는 일을 해야 정직해지며 삶을 더 즐길 줄
                알게 된다. 다름 사람에게도 정직해야 하지만 그 무엇보다 나
                자신한테 정직해야 한다.
              </p>
            </div>
            <img
              src="https://github.com/mj0614k/react_api/blob/main/src/assets/img/aboutImg03.jpg?raw=true"
              alt="이미지3"
            />
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
export default {
  components: {
    HeaderCont,
    TitleCont,
    ContactCont,
    FooterCont,
  },
};
</script>
<style lang="scss">
.cont__about1 {
  img {
    margin-bottom: 60px;
  }
  h2 {
    font-family: var(--font-kor);
    color: var(--black);
    font-size: 18px;
    font-weight: 600;
    margin-bottom: 20px;
  }
  p {
    line-height: 1.6;
    font-size: 18px;
    color: var(--black);
    font-family: var(--font-kor);
  }
  margin-bottom: 240px;
}
.cont__about2 {
  display: flex;
  .cont__layout {
    display: flex;
    flex-direction: column;
    width: 40%;
  }
  img {
    margin-right: 60px;
    width: 60%;
  }
  h2 {
    font-family: var(--font-kor);
    color: var(--black);
    margin-bottom: 20px;
    font-weight: 600;
    font-size: 18px;
  }
  p {
    line-height: 1.6;
    font-size: 18px;
    color: var(--black);
    font-family: var(--font-kor);
  }
  margin-bottom: 240px;
}
.cont__about3 {
  display: flex;
  .cont__layout {
    display: flex;
    flex-direction: column;
    width: 40%;
  }
  img {
    margin-left: 60px;
    width: 60%;
  }
  h2 {
    font-family: var(--font-kor);
    color: var(--black);
    margin-bottom: 20px;
    font-size: 18px;
    font-weight: 600;
  }
  p {
    line-height: 1.6;
    font-size: 18px;
    color: var(--black);
    font-family: var(--font-kor);
  }
}
</style>
