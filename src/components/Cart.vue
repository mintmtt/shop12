<template>
  <div>
    <b-container>
      <b-row>
        <b-col>
          <h5 style="padding-bottom:50px ; padding-top:60px">รายการสินค้า</h5>
        </b-col>
      </b-row>

      <b-row>
        <b-col v-for="product in products" :key="product.id">
          <b-card no-body class="overflow-hidden" style=" width: 350px; margin-bottom:20px">
            <b-row no-gutters>
              <b-col md="6">
                <b-card-img
                  :src="require(`@/assets/flower${product.id}.jpeg`)"
                  alt="Image"
                  class="rounded-0"
                ></b-card-img>
              </b-col>
              <b-col md="6">
                <b-card-body :title="product.name">
                  <b-card-text>
                    ราคา {{ product.price }} บาท
                  </b-card-text>
                  <b-button
                    v-if="!product.cart"
                    @click="add(product)"
                    href="#"
                    variant="outline-dark"
                    size="sm"
                    >เพิ่มสินค้า</b-button
                  >
                  <b-button
                    v-if="product.cart"
                    @click="add(product)"
                    :disabled="product.cart"
                    href="#"
                    variant="outline-success"
                    size="sm"
                    >เพิ่มสินค้าเรียบร้อย
                  </b-button>
                </b-card-body>
              </b-col>
            </b-row>
          </b-card>

        </b-col>
      </b-row>

      <b-row>
        <b-col>
          <h5 style="padding-top:80px ; padding-bottom:40px">Shopping Cart</h5>
        </b-col>
      </b-row>

      <b-row>
        <b-col>
          <b-table bordered hover :items="cart" :fields="fields">
            <template slot="#" slot-scope="data">
              {{ data.index + 1 }}
            </template>
            <template slot="price" slot-scope="data">
              {{ data.item.price * data.item.quantity }}
            </template>
            <template slot="remove" slot-scope="data">
              <b-button
                @click="remove(data.item.id)"
                variant="outline-danger"
                class="mr-2"
              >
                X
              </b-button>
            </template>
            <template slot="quantity" slot-scope="data">
              <b-row>
                <b-col cols="5">
                  <b-button
                    :disabled="data.item.quantity <= 1"
                    variant="outline-primary"
                    @click="decrement(data.item.id)"
                    class="mr-2"
                  >
                    -
                  </b-button>
                </b-col>
                <b-col cols="2">
                  <h4>{{ data.item.quantity }}</h4>
                </b-col>
                <b-col cols="5">
                  <b-button
                    variant="outline-primary"
                    @click="increment(data.item.id)"
                    class="mr-2"
                  >
                    +
                  </b-button>
                </b-col>
              </b-row>
            </template>

            <template slot="image" slot-scope="data">
              <b-img
                style="max-width: 5rem;"
                :src="require(`@/assets/flower${data.item.id}.jpeg`)"
                fluid
                alt="Responsive image"
              ></b-img>
            </template>
          </b-table>
        </b-col>
      </b-row>
      <b-row v-if="cart.length > 0">
        <b-col></b-col>
        <b-col></b-col>
        <b-col></b-col>
        <b-col></b-col>
        <b-col><h5>รวม</h5></b-col>
        <b-col
          ><h5>{{ total }} บาท</h5></b-col
        >
      </b-row>
      <b-row v-if="cart.length > 0">
        <b-col>
          <b-button @click="clean" variant="outline-danger" block class="mr-2">
            Clean
          </b-button>
        </b-col>
        <b-col></b-col>
        <b-col cols="4"></b-col>

        <b-col> </b-col>
        <b-col>
          <b-button @click="buy" variant="outline-success" block class="mr-2">
            Buy
          </b-button>
        </b-col>
      </b-row>
      <b-modal
        hide-header-close
        no-close-on-esc
        no-close-on-backdrop
        ref="modal-1"
        centered
        title="Purchase Completed "
      >
        <template slot="modal-footer">
          <b-button class="mt-3" variant="outline-secondary" block @click="clean"
            >Close</b-button
          >
        </template>
        <p class="my-4">รายการสินค้า</p>
        <ul v-for="productFinal in ticket.products" :key="productFinal.id">
          <li>Product name: {{ productFinal.name }}</li>
          <li>Quantity: {{ productFinal.quantity }}</li>
          <li>Price: {{ productFinal.price }}</li>
          <li>Total: {{ productFinal.price * productFinal.quantity }}</li>
          <hr />
        </ul>
        <h5 class="my-4">รวม {{ ticket.total }} บาท</h5>
      </b-modal>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "Cart",
  props: {
    msg: String,
  },
  data() {
    return {
      ticket: {
        products: null,
        total: 0,
      },
      counter: 0,
      products: [
        {
          id: 1,
          img: "@/assets/flower1.jpeg",
          name: "True Love",
          price: 3790,
          cart: false,
          quantity: 1,
        },
        {
          id: 2,
          img: "@/assets/flower2.jpeg",
          name: "Pure",
          price: 2890,
          cart: false,
          quantity: 1,
        },
        {
          id: 3,
          img: "@/assets/flower3.jpeg",
          name: "Ella",
          price: 2350,
          cart: false,
          quantity: 1,
        },
        {
          id: 4,
          img: "@/assets/flower4.jpeg",
          name: "Ella",
          price: 2350,
          cart: false,
          quantity: 1,
        },
        {
          id: 5,
          img: "@/assets/flower5.jpeg",
          name: "Genesis",
          price: 2590,
          cart: false,
          quantity: 1,
        },
          {
          id: 6,
          img: "@/assets/flower6.jpeg",
          name: "Izabela",
          price: 2490,
          cart: false,
          quantity: 1,
        },
        {
          id: 7,
          img: "@/assets/flower7.jpeg",
          name: "Valentine",
          price: 2690,
          cart: false,
          quantity: 1,
        },
        {
          id: 8,
          img: "@/assets/flower8.jpeg",
          name: "Arista",
          price: 7590,
          cart: false,
          quantity: 1,
        },
          {
          id: 9,
          img: "@/assets/flower9.jpeg",
          name: "Chana",
          price: 9990,
          cart: false,
          quantity: 1,
        },
        ],
      cart: [],
      fields: ["#", "remove", "image", "name", "quantity", "price"],
    }; // data return
  },
  methods: {
    add(product) {
      this.products[product.id - 1].cart = true;
      this.cart.push(product);
      this.counter++;
    },
    clean() {
      this.cart = [];

      for (const key in this.products) {
        this.products[key].cart = false;
        this.products[key].quantity = 1;
      }
      this.$refs["modal-1"].hide();
    },
    remove(id) {
      for (let index = 0; index < this.products.length; index++) {
        if (this.products[index].id == id) {
          this.products[index].cart = false;
        }
      }
      for (let index = 0; index < this.cart.length; index++) {
        if (this.cart[index].id == id) {
          this.cart.splice(index, 1);
        }
      }
    },
    buy() {
      this.ticket = {
        products: this.cart,
        total: this.total,
      };
      this.$refs["modal-1"].show();
    },
    increment(id) {
      for (let index = 0; index < this.cart.length; index++) {
        if (this.cart[index].id == id) {
          this.cart[index].quantity++;
        }
      }
    },
    decrement(id) {
      for (let index = 0; index < this.cart.length; index++) {
        if (this.cart[index].id == id) {
          this.cart[index].quantity--;
        }
      }
    },
  },
  computed: {
    total() {
      let t = 0;
      for (let index = 0; index < this.cart.length; index++) {
        t += this.cart[index].price * this.cart[index].quantity;
      }
      return t;
    },
  },
};
</script>

<style scoped></style>
