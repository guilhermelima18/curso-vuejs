<template>
  <div>
    <div>
      <img :src="dados.avatar_url" :alt="dados.name" />
      <p>Nome: {{ dados.name }}</p>
      <p>Repositórios Públicos: {{ dados.public_repos }}</p>
      <p>Data de Criação: {{ formatDate(dados.created_at) }}</p>
    </div>
  </div>
  <div>
    <button @click="contador++">Contador: {{ contador }}</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      dados: {
        avatar_url: "",
        name: "",
        public_repos: 0,
        created_at: "",
      },
      contador: 0,
    };
  },
  methods: {
    formatDate(data) {
      return new Date(data).toLocaleDateString("pt-BR", {
        day: "2-digit",
        month: "2-digit",
        year: "numeric",
      });
    },
    async getData() {
      const response = await axios.get(
        "https://api.github.com/users/guilhermelima18"
      );

      if (response.status === 200) {
        this.dados = {
          avatar_url: response.data.avatar_url,
          name: response.data.name,
          public_repos: response.data.public_repos,
          created_at: response.data.created_at,
        };
      }
    },
  },
  created() {
    this.getData();
  },
  updated() {
    window.document.title = this.contador;
  },
};
</script>
