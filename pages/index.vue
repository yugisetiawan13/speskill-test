<template>
  <div>
    <v-container>
      <v-card>
        <v-simple-table>
          <template v-slot:default>
            <thead style="background-color: black">
              <tr>
                <th class="text-center white--text" width="20%"></th>
                <th class="text-center white--text" width="40%">Product</th>
                <th class="text-center white--text" width="20%">Quantity</th>
                <th class="text-center white--text" width="20%">Subtotal</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(val, i) in cars" :key="i">
                <td width="20%">
                  <img :src="val.product.media_url" alt="" width="100%" />
                </td>
                <td width="40%">
                  <h5 class="primary--text">{{ val.product.code }}</h5>
                  <h5 class="font-weight-bold">{{ val.product.name }}</h5>
                  <h5 class="grey--text">IDR.{{ val.product.price }}</h5>
                  <h5 class="red--text">{{ val.product.stock }} in Stock</h5>
                </td>
                <td class="text-center" width="20%">{{ val.quantity }}</td>
                <td class="text-center" width="20%">
                  IDR.{{ val.product.price * val.quantity }}
                </td>
              </tr>
            </tbody>
            <thead style="background-color: black">
              <tr>
                <th class="text-center white--text" width="20%"></th>
                <th class="text-center white--text" width="40%"></th>
                <th class="text-center white--text" width="20%">Total</th>
                <th class="text-center white--text" width="20%"></th>
              </tr>
            </thead>
          </template>
        </v-simple-table>
      </v-card>
    </v-container>
  </div>
</template>
<script>
export default {
  name: "IndexPage",
  data() {
    return {
      cars: [],
    };
  },
  async fetch() {
    const token = "o7Ytbt9XQLI3PgtebJfKSXKEf0XHU74Y";
    this.cars = await this.$axios
      .$get("https://spe-academy.spesolution.net/api/recruitment", {
        headers: {
          "Content-Type": "application/json",
          Authorization: "Bearer " + token,
        },
      })
      .then((res) => res);

    console.log(this.cars);
  },
  computed: {
    countTotal() {
      const subtotal = this.cars.product.price * this.cars.quantity;
      let total = subtotal * this.cars.length;

      return total;
    },
  },
};
</script>
