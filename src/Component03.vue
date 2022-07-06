<script>
export default {
  data() {
    return {
      totalItens: 7,
      totalCarrinho: 0,
      itensEstoque: ["Banana", "Maça", "Morango", "Uva", "Pêssego"],
      itensCarrinho: [],
    };
  },
  methods: {
    adicionarCarrinho() {
      this.totalCarrinho++;
      this.totalItens--;
    },
    removerCarrinho() {
      this.totalCarrinho--;
      this.totalItens++;
    },
    adicionarItemCarrinho(item) {
      if (this.itensCarrinho.includes(item)) {
        return;
      }

      this.itensCarrinho = [...this.itensCarrinho, item];
    },
    removerItemCarrinho(index) {
      this.itensCarrinho.splice(index, 1);
    },
  },
};
</script>

<template>
  <div>
    <div>
      <p>Total de itens no carrinho: {{ totalCarrinho }}</p>
    </div>
    <div v-show="totalItens > 0">
      <button @click="adicionarCarrinho">+</button>
      <button @click="removerCarrinho">-</button>
    </div>
    <div v-if="totalItens > 0">
      <p>Total de itens no estoque: {{ totalItens }}</p>
      <button @click="adicionarCarrinho">Adicionar item ao carrinho</button>
    </div>
    <div v-else>
      <h1>Sem estoque</h1>
    </div>
    <div>
      <ul>
        <li :key="item" v-for="item in itensEstoque">
          {{ item }}
          <button @click="adicionarItemCarrinho(item)">Adicionar</button>
        </li>
      </ul>
    </div>
    <div v-if="itensCarrinho.length > 0">
      <ul>
        <li :key="itemCarrinho" v-for="(itemCarrinho, index) in itensCarrinho">
          {{ itemCarrinho }}
          <button @click="removerItemCarrinho(index)">Remover</button>
        </li>
      </ul>
    </div>
  </div>
</template>
