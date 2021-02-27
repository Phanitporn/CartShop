<template>
  <div id="app">
    <div class="container">
      <hr />
      <div class="row">
        <div class="col-md-3 " v-for="item in products" :key="item">
          <b-card
            :img-src="item.image"
            img-alt="Image"
            img-top
            tag="article"
            style="max-width: 20rem"
            class="mb-2 my-3 text-center"
          >
            <h6 class="text-left" style="color:navy ">{{ item.name }}</h6>
            <b-card-text class="text-left" style="color:orangered ">
              ราคา {{ item.price }} THB.
            </b-card-text>

            <b-button href="#" variant="primary" @click="addCart(item)"
              >หยิบใส่ตะกร้า</b-button
            >
          </b-card>
        </div>
        <div class="col-md-8 " v-if="carts != 0">
          <h4>
            ตะกร้าสินค้า
            <i class="fa fa-shopping-cart"></i>
          </h4>
          <hr />
          <table class="table">
            <thead class="thead-dark">
              <tr>
                <th scope="col">ภาพ</th>
                <th scope="col">ชื่อ</th>
                <th scope="col">ราคา</th>
                <th scope="col">จำนวน</th>
                <th scope="col">ยอดรวม</th>
                <th scope="col">ลบ</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="product in carts" :key="product">
                <td>
                  <img
                    :src="product.image"
                    alt=""
                    width="80px"
                    height="100px"
                  />
                </td>
                <td>{{ product.name }}</td>
                <td>{{ product.price }}</td>
                <td>
                  <i
                    class="fa fa-minus qty-minus"
                    @click="minusQty(product)"
                  ></i>
                  {{ product.qty }}
                  <i class="fa fa-plus qty-plus" @click="plusQty(product)"></i>
                </td>
                <td>{{ product.total }}</td>
                <td>
                  <button @click="removeProduct(product)" class="btn-danger">
                    <!-- <i class="fa fa-trash"></i> -->
                  </button>
                </td>
              </tr>
              <!-- <button class="align-center">ซื้อสินค้า</button> -->
            </tbody>
          </table><div>
          <h4 align="right">ยอดชำระเงิน {{ total() }} บาท</h4>

            <!-- <button class="checkoutCart" v-show="checkoutBool" @click="propagateCheckout()"> Checkout </button> -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Cart",
  data() {
    return {
      carts: [],
      pd1: 0,
      pd2: 0,
      pd3: 0,
      pd4: 0,
      pd5: 0,
      pd6: 0,
      pd7: 0,
      pd8: 0,
      products: [
        {
          id: 1,
          name: "เคส iPhone พิมพ์ลายเปลวไฟ",
          price: 85,
          image:
            "https://img.ltwebstatic.com/images3_pi/2020/12/23/16087037745f3a628dd09bbe0c746035ef3ac5de4d_thumbnail_600x.webp",
          active: false,
        },
        {
          id: 2,
          name: " เคส iPhone พิมพ์ลาย",
          price: 70,
          image:
            "https://img.ltwebstatic.com/images3_pi/2021/01/08/1610085416f3ab0a7ea6cc9849f814a19fa05e74ff_thumbnail_600x.webp",
          active: false,
        },
        {
          id: 3,
          name: "เคส iPhone จับคู่สี",
          price: 45,
          image:
            "https://img.ltwebstatic.com/images3_pi/2020/12/23/1608703585d95b13b816cef24303b79a9e37be35f3_thumbnail_600x.webp",
          active: false,
        },
        {
          id: 4,
          name: "เคส iPhone ลายเมฆ",
          price: 120,
          image:
            "https://img.ltwebstatic.com/images3_pi/2021/01/05/1609817927f24bab4c95b7ea5fa2a1af2cf15a6f5d_thumbnail_600x.webp",
          active: false,
        },
        {
          id: 5,
          name: " เคส iPhone พิมพ์ลายแมว",
          price: 40,
          image:
            "https://img.ltwebstatic.com/images3_pi/2020/10/27/1603781050ca6f4af843164a80336ff6a53f47fbc5_thumbnail_600x.webp",
          active: false,
        },
        {
          id: 6,
          name: "เคส iPhone แบบเกมคอนโซล",
          price: 50,
          image:
            "https://img.ltwebstatic.com/images3_pi/2021/01/08/16100770260532ecfa81d364d0cd06ef7e4dbec270_thumbnail_600x.webp",
          active: false,
        },
        {
          id: 7,
          name: " เคส iPhone ลายกราฟฟิก",
          price: 79,
          image:
            "https://img.ltwebstatic.com/images3_pi/2020/10/21/1603269119e897e76dfde7cb3cb6684be9ad7700d3_thumbnail_600x.webp",
          active: false,
        },
        {
          id: 8,
          name: "เคส iPad ลายหินอ่อน",
          price: 139,
          image:
            "https://img.ltwebstatic.com/images3_pi/2020/06/22/1592800433ecf45d453cd2df5034586710c901801c_thumbnail_600x.webp",
          active: false,
        },
      ],
    };
  },
  methods: {
    addCart: function(item) {
      var found = false;

      if (item.id == 1) {
        this.pd1 += 1;
        if (this.pd1 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (item.id == 2) {
        this.pd2 += 1;
        if (this.pd2 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (item.id == 3) {
        this.pd3 += 1;
        if (this.pd3 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (item.id == 4) {
        this.pd4 += 1;
        if (this.pd4 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (item.id == 5) {
        this.pd5 += 1;
        if (this.pd5 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (item.id == 6) {
        this.pd6 += 1;
        if (this.pd6 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (item.id == 7) {
        this.pd7 += 1;
        if (this.pd7 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (item.id == 8) {
        this.pd8 += 1;
        if (this.pd8 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      }
    },
    pushData(item) {
      this.carts.push({
        id: item.id,
        name: item.name,
        price: item.price,
        image: item.image,
        qty: 1,
        total: item.price,
      });
    },
    findIndex: function(item) {
      for (var i = 0; i < this.carts.length; i++) {
        if (this.carts[i].id == item.id) {
          return i;
        }
      }
      return -1;
    },
    minusQty: function(product) {
      product.qty -= 1;
      if (product.qty <= 1) {
        product.qty = 1;
      }
      product.total = product.price * product.qty;
    },
    plusQty: function(product) {
      product.qty += 1;
      product.total = product.price * product.qty;
    },
    removeProduct(product) {
      if (confirm("คุณต้องการลบหรือไม่ ?")) {
        var index = this.carts.indexOf(product);
        this.carts.splice(index, 1);
        if (product.id == 1) {
          this.pd1 = 0;
        } else {
          this.tea = 0;
        }
      }
    },
    total: function() {
      var sum = 0;
      this.carts.forEach(function(item) {
        sum += item.total;
      });
      return sum;
    },
  },
};
</script>
<style scoped>
.qty-minus {
  cursor: pointer;
  margin-right: 20px;
}
.qty-plus {
  cursor: pointer;
  margin-left: 20px;
}
/* .checkout-area table {
  margin: 0 auto;
  padding: 0.5em;
  width: 100%;
  max-width: 40em;
  text-align: left;
}
.checkout-area table th, .checkout-area table td {
  padding: 0 0.25em;
}
@media (max-width: 600px) {
  .checkout-area table th:nth-child(3), .checkout-area table td:nth-child(3) {
    display: none;
  }
} */
</style>
