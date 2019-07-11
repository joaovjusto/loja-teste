<template>
  <div class="container">
    <div class="row">
      <div class="col-6 custom-height">
        <div class="title">
          <h3>Games</h3>
        </div>
      </div>
      <div class="col-3 custom-height">
        <div class="filter">
          <el-select v-model="filtro" placeholder="Filtro">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </div>
      </div>
      <div class="col-3 custom-height">
        <div class="cart-box">
          <div class="card-title">
            <h3>Carrinho</h3>
          </div>
          <div class="cart-empty" v-if="emptyCart">
            <div class="img-cart">
              <img class="img-cart" src="../assets/cart-icon.svg" alt />
            </div>
            <p>Até o momento o seu carrinho está vazio</p>
          </div>
        </div>
      </div>
      <div class="col-9">
        <div class="row">
          <div class="col-4" v-for="item in sortedArray" :key="item.id">
            <el-card :body-style="{ padding: '0px' }">
              <img :src="require(`../assets/${item.image}`)" class="image" />
              <div class="text-center" style="padding: 15px;">
                <span>{{item.name}}</span>
                <div class="bottom clearfix text-center">
                  <time class="time">{{"R$ " + monetary(item.price)}}</time>
                </div>
              </div>
            </el-card>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const content = require("../content/products.json");

export default {
  name: "principal",
  data() {
    return {
      itens: content,
      options: [
        {
          value: "name",
          label: "Ordem Alfabética"
        },
        {
          value: "score",
          label: "Mais Populares"
        },
        {
          value: "price",
          label: "Menor Preço"
        }
      ],
      filtro: "name",
      emptyCart: true
    };
  },
  methods: {
    monetary(num) {
      var value = Number(num);

      num = num + "";
      var res = num.split(".");
      if (res.length == 1 || res[1].length < 3) {
        value = value.toFixed(2);
      }

      var ret = value.replace(".", ",");
      return ret;
    }
  },
  computed: {
    sortedArray: function() {
      if (this.filtro == "name") {
        function compare(a, b) {
          if (a.name < b.name) return -1;
          if (a.name > b.name) return 1;
          return 0;
        }

        return this.itens.sort(compare);
      } else if (this.filtro == "price") {
        function compare(a, b) {
          if (a.price < b.price) return -1;
          if (a.price > b.price) return 1;
          return 0;
        }

        return this.itens.sort(compare);
      } else if (this.filtro == "score") {
        function compare(a, b) {
          if (a.score < b.score) return -1;
          if (a.score > b.score) return 1;
          return 0;
        }

        return this.itens.sort(compare);
      }
    }
  }
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css?family=Open+Sans");

img {
  user-select: none;
  -moz-user-select: none;
  -webkit-user-drag: none;
  -webkit-user-select: none;
  -ms-user-select: none;
}
.el-card.is-always-shadow {
  box-shadow: none !important;
}
.el-card {
  margin-bottom: 20px;
  border: none;
}
.el-card__body span {
  font-family: "Open Sans";
  font-weight: 500;
  text-align: center;
  font-size: 16px;
  color: #746a6a;
  margin-top: 10px;
}
.el-card__body img {
  background-color: #eeeeee;
  padding: 40px;
  border-radius: 5px;
}
.el-card__body .time {
  font-family: "Open Sans";
  font-weight: 600;
  text-align: center;
  font-size: 16px;
  color: #3486e6;
  margin-top: 10px;
}
.custom-height {
  height: 120px;
}
.cart-empty p {
  font-family: "Open Sans";
  text-align: center;
  font-size: 14px;
  color: #746a6a;
  margin-top: 20px;
}
.img-cart {
  text-align: center;
  margin-top: 30px;
}
.card-title h3 {
  font-family: "Open Sans";
  font-weight: 600;
  font-size: 20px;
}
.cart-box {
  border: 1px solid #e1e1e1;
  border-radius: 5px;
  margin: 42px 70px 42px 0;
  width: 260px;
  height: 360px;
  padding: 20px;
}
.title h3 {
  font-family: "Open Sans";
  font-weight: bold;
  font-size: 45px;
  color: #363636;
  margin: 35px 0 42px 0;
}
.filter {
  margin: 42px 30px;
}
</style>

