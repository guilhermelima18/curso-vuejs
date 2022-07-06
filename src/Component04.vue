<template>
  <div>
    <button @click="getPaises">Buscar países</button>
  </div>
  <div>
    <select name="paises" id="paises" v-model="paisSelecionado">
      <option
        :value="pais.nativeName"
        :key="pais.nativeName"
        v-for="pais in paises"
      >
        {{ pais.nativeName }}
      </option>
    </select>
  </div>
  <div>
    <main :key="data.nativeName" v-for="data in pais">
      <h1>Nome: {{ data.nativeName }}</h1>
      <h4>Capital: {{ data.capital }}</h4>
      <p>População: {{ data.population }}</p>
    </main>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      pais: [],
      paises: [],
      paisSelecionado: "",
    };
  },
  methods: {
    async getPaises() {
      const response = await axios.get("https://restcountries.com/v2/all");

      if (response.status === 200) {
        this.paises = response.data;
      }
    },
  },
  watch: {
    async paisSelecionado(pais) {
      const response = await axios.get(
        `https://restcountries.com/v2/name/${pais}`
      );

      if (response.status === 200) {
        this.pais = response.data;
      }
    },
  },
};
</script>
