<template>
  <div class="page">
    <section class="find_all">
      <div class="container">
        <div class="row">
          <div class="col-xl-7 col-12">
            <div class="description">
              <h1>{{ title }}</h1>
              <p>{{ description }}</p>

              <ul class="nav">
                <li role="presentation" @click="getTomatoes(); currentTab = 'tomato'">Помидоры
                </li>
                <li role="presentation" @click="getCats(); currentTab = 'cats'">Коты
                </li>
                <li role="presentation" @click="getSocks(); currentTab = 'socks'">Носки
                </li>
              </ul>
            </div>
          </div>
          <div class="col-xl-5 col-12">
            <img src="../assets/img/CreativeBlock.png" alt="" />
          </div>
        </div>
      </div>
    </section>

    <section class="result">
      <div id="tomato" v-if="currentTab == 'tomato'">
        <div class="container">
          <div
            v-for="tomato of tomatoes"
            :key="tomato.id"
            class="row card_item">
            <div class="col-xl-5 col-12">
              <img :src="tomato.image" />
            </div>
            <div class="col-xl-6 col-12">
              <h2>{{ tomato.name }}</h2>
              <p>
                {{ tomato.description }}
              </p>
              <span>{{ tomato.price }} руб.</span>
            </div>
          </div>
        </div>
      </div>
      <div id="cats" v-if="currentTab == 'cats'">
        <div class="container">
          <div class="row">
            <div
              v-for="cat of cats"
              :key="cat.id"
              class="col-xl-5 col-12 card_item">
              <img :src="cat.image" />
              <h2>{{ cat.name }}</h2>
              <ul>
                <li v-for="item in cat.advantages" :key="item">{{ item }}</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
      <div id="socks" v-if="currentTab == 'socks'">
        <div class="container">
          <div class="row">
            <div
              v-for="sock of socks"
              :key="sock.id"
              class="col-xl-5 col-12 card_item">
              <swiper ref="mySwiper" >
                <swiper-slide v-for="item in sock.images" :key="item"
                  ><img :src="item" alt=""
                /></swiper-slide>
              </swiper>

              <h2>{{ sock.name }}</h2>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>



<script>
export default {
  data() {
    return {
      tomatoes: [],
      cats: [],
      socks: [],
      title: "Найдется всё!",
      description:
        "Самые важные вещи для качественной жизни. Ласковые коты, вкусные помидоры и умопомрачительные носки!",
      currentTab: "tomato",
    };
  },
  methods: {
    getTomatoes() {
      this.$axios.$get("https://eon.estate/api/v0/tomatoes").then((res) => {
        this.tomatoes = res;
      });
    },
    getCats() {
      this.$axios.$get("https://eon.estate/api/v0/cats").then((res) => {
        this.cats = res;
      });
    },
    getSocks() {
      this.$axios.$get("https://eon.estate/api/v0/socks").then((res) => {
        this.socks = res;
      });
    },
  },
};
</script>


<style>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap");
html,
body {
  font-family: "Inter", sans-serif;
  font-weight: 400;
  font-size: 18px;
  background: #e5e5e5;
}
h1 {
  font-size: 72px;
  font-weight: 800;
}
h2 {
  margin-top: 25px;
  font-size: 24px;
  font-weight: 600;
}
.find_all {
  background: #18191f;
  color: #fff;
}
.find_all .row {
  align-items: center;
}

.find_all p {
  margin-top: 50px;
}

.nav {
  margin-top: 50px;
  justify-content: space-between;
}

.nav li {
  margin: 0 10px;
  padding: 20px;
  flex-grow: 1;
  text-align: center;
  background: linear-gradient(44.11deg, #cd10ff 15.75%, #9f06ff 84.63%);
  border-radius: 33px;
  color: #fff;
}

.nav li:hover {
  background: linear-gradient(44.11deg, #10c6ff 15.75%, #9f06ff 84.63%);
  cursor: pointer;
}


.result {
  margin: 70px 0 300px;
}
.card_item {
  margin: 0px 20px 50px 20px;
  padding: 25px;
  box-shadow: 0px 0px 1px rgba(12, 26, 75, 0.24),
    0px 3px 8px -1px rgba(50, 50, 71, 0.05);
}
.card_item img {
  width: 100%;
}

.card_item p,
.card_item span {
  margin-top: 20px;
}

.card_item span {
  font-weight: 700;
}

.card_item ul {
  padding-left: 0;
  list-style-type: none;
}

.card_item ul li:before {
  content: "— ";
}
</style>
