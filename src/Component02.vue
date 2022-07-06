<script type="module">
import axios from "axios";

export default {
  data() {
    return {
      companyOne: {
        companyName: "",
        marketCap: 0,
      },
      companyTwo: {
        companyName: "",
        marketCap: 0,
      },
    };
  },
  methods: {
    async getPrices() {
      const getCompanyOne = await axios.get(
        "https://cloud.iexapis.com/stable/stock/aapl/quote?token=sk_e63458ef22d140b7a0e3d0e91cfe7b4a"
      );

      const getCompanyTwo = await axios.get(
        "https://cloud.iexapis.com/stable/stock/googl/quote?token=sk_e63458ef22d140b7a0e3d0e91cfe7b4a"
      );

      const [companyOne, companyTwo] = await Promise.all([
        getCompanyOne,
        getCompanyTwo,
      ]);

      if (companyOne.status === 200 && companyTwo.status === 200) {
        this.companyOne.companyName = companyOne.data.companyName;
        this.companyOne.marketCap = companyOne.data.marketCap;
        this.companyTwo.companyName = companyTwo.data.companyName;
        this.companyTwo.marketCap = companyTwo.data.marketCap;
      }
    },
    formatPrice(value) {
      return value.toLocaleString("pt-BR", {
        style: "currency",
        currency: "BRL",
      });
    },
    formatData(data) {
      return new Date(data).toLocaleDateString("pt-BR", {
        day: "2-digit",
        month: "2-digit",
        year: "numeric",
      });
    },
  },
};
</script>

<template>
  <div>
    <div
      :class="
        companyOne.marketCap === 0
          ? 'white'
          : companyOne.marketCap > companyTwo.marketCap
          ? 'green'
          : 'red'
      "
    >
      <p>Company Name: {{ companyOne.companyName }}</p>
      <p>Market Cap: {{ companyOne.marketCap }}</p>
    </div>
    <div
      :class="
        companyTwo.marketCap === 0
          ? 'white'
          : companyTwo.marketCap > companyOne.marketCap
          ? 'green'
          : 'red'
      "
    >
      <p>Company Name: {{ companyTwo.companyName }}</p>
      <p>Market Cap: {{ companyTwo.marketCap }}</p>
    </div>
    <button @click="getPrices">Ver preço</button>
  </div>
</template>

<style scoped>
.white {
  background: white;
}

.green {
  background: green;
}

.red {
  background: red;
}
</style>
