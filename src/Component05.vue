<template>
  <div v-if="isCreated">
    <h3>Nome: {{ createUser.name }}</h3>
    <h3>E-mail: {{ createUser.email }}</h3>
    <h3>Telefone: {{ createUser.phone }}</h3>
    <h3>Mensagem: {{ createUser.message }}</h3>
  </div>
  <form v-else @submit="handleFormSubmit">
    <div class="formGroup">
      <div>
        <label for="name">Nome</label>
        <input type="text" id="name" v-model="createUser.name" />
      </div>
      <div>
        <label for="phone">Telefone</label>
        <input type="text" id="phone" v-model="createUser.phone" />
      </div>
    </div>
    <div class="formGroup">
      <div>
        <label for="email">E-mail</label>
        <input type="email" id="email" v-model="createUser.email" />
      </div>
    </div>
    <div>
      <label for="message">Mensagem</label>
      <textarea id="message" v-model="createUser.message" />
    </div>
    <button type="submit">Enviar</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      createUser: {
        name: "",
        email: "",
        phone: "",
        message: "",
      },
      isCreated: false,
    };
  },
  methods: {
    handleFormSubmit(event) {
      event.preventDefault();

      if (
        this.createUser.name &&
        this.createUser.email &&
        this.createUser.phone &&
        this.createUser.message
      ) {
        this.isCreated = true;
      } else {
        alert("Preencha todos os campos");
      }
    },
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}

form {
  width: 50%;
  height: 50%;
  margin: 5rem auto;
  display: flex;
  flex-direction: column;
}

form button {
  background: green;
  width: 300px;
  height: 50px;
  outline: none;
  border: none;
  border-radius: 5px;
  font-size: 1rem;
  font-weight: bold;
  color: white;
  margin: 2rem auto;
  transition: 500ms;
  cursor: pointer;
}

form button:hover {
  background: rgb(1, 95, 1);
}

.formGroup {
  width: 100%;
  display: flex;
}

.formGroup div {
  flex: 1;
  margin: 1rem 0;
  display: flex;
  flex-direction: column;
}

.formGroup div + div {
  margin-left: 10px;
}

.formGroup div label,
form div label {
  font-size: 1rem;
  font-weight: bold;
}

.formGroup div input,
form div textarea {
  width: 100%;
  height: 40px;
  border: 1px solid rgba(200, 200, 200, 0.5);
  border-radius: 5px;
  margin-top: 0.3rem;
  outline: none;
  padding: 0 1rem;
}

form div textarea {
  resize: none;
  height: 100px;
  padding: 1rem;
}

.formGroup div input:focus,
form div textarea:focus {
  border: 2px solid;
  border-color: rgb(78, 78, 245);
}
</style>
