<template>
  <div>
    <div class="container-fluid cart-container">
      <div class="row">
        <div class="col-md-6">
          <div class="box-container">
            <h2 class="cart-title">Products</h2>
            <div class="product" v-for="product in products" :key="product.id">
              <h3>{{ product.name }}</h3>
              <p>Price: ₱{{ product.price }}</p>
              <button
                v-if="isLoggedIn"
                class="btn btn-primary"
                @click="addToCart(product)"
              >
                Add to Cart
              </button>
              <button v-else class="btn btn-primary" disabled>
                Login to add to cart
              </button>
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <div class="box-container" style="height: 400px; overflow-y: auto">
            <h2 class="cart-title">Cart</h2>
            <div class="cart-item" v-for="item in cart" :key="item.product.id">
              <span>{{ item.product.name }}</span>
              <input
                v-if="isLoggedIn"
                type="number"
                class="form-control"
                v-model="item.quantity"
                min="1"
                @change="updateCart"
              />
              <input
                v-else
                type="number"
                class="form-control"
                v-model="item.quantity"
                min="1"
                disabled
              />
              <button
                v-if="isLoggedIn"
                class="btn btn-danger"
                @click="removeFromCart(item.product)"
              >
                Remove
              </button>
            </div>
          </div>
          <br />
          <h3>Total: ₱{{ total }}</h3>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
    isLoggedIn: Boolean,
  },

  data() {
    return {
      products: [
        { id: 1, name: "iDoll Sun", price: 500 },
        { id: 2, name: "Bauxite", price: 45 },
        { id: 3, name: "Ammo (Box)", price: 120 },
        { id: 4, name: "Steel", price: 20 },
        { id: 5, name: "Fuel", price: 59 },
      ],
      cart: [],
    };
  },

  methods: {
    addToCart(product) {
      const existingItem = this.cart.find(
        (item) => item.product.id === product.id
      );
      if (existingItem) {
        existingItem.quantity++;
      } else {
        this.cart.push({ product: product, quantity: 1 });
      }
      this.saveCartToStorage(); // Save cart to localStorage
    },
    removeFromCart(product) {
      const index = this.cart.findIndex(
        (item) => item.product.id === product.id
      );
      if (index !== -1) {
        this.cart.splice(index, 1);
        this.saveCartToStorage(); // Save cart to localStorage
      }
    },
    saveCartToStorage() {
      localStorage.setItem("cart", JSON.stringify(this.cart)); // Save cart to localStorage
    },
    getCartFromStorage() {
      const cart = localStorage.getItem("cart");
      if (cart) {
        this.cart = JSON.parse(cart); // Retrieve cart from localStorage
      }
    },
  },

  computed: {
    total() {
      return this.cart.reduce(
        (acc, item) => acc + item.product.price * item.quantity,
        0
      );
    },
  },

  created() {
    this.getCartFromStorage(); // Retrieve cart from localStorage when component is created
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.cart-container {
  margin-top: 5%;
  border-style: dashed;
}
.cart-title {
  text-align: center;
}
</style>
