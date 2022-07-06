<script>
export default {
  data() {
    return {
      nome: "",
      preco: 50,
      quantidade: 0,
      precoTotal: 0,
    };
  },

  computed: {
    nomeProduto() {
      setTimeout(() => {
        // This da arrow function se refere ao objeto VUE
        // This em funções de callback se refere ao objeto WINDOW
        return (this.nome = "Camisa");
      }, 1000);
    },
  },

  methods: {
    increment() {
      this.quantidade++;
      this.precoTotal += this.preco * this.quantidade;
    },
    decrement() {
      this.precoTotal -= this.preco * this.quantidade;
      this.quantidade--;
    },
  },
};
</script>
