<template>
  <h3>Adicionar transação</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Descrição</label>
      <input type="text" id="text" placeholder="Inserir descrição" v-model="text" />
    </div>
    <div class="form-control">
      <label for="amount"
        >Valor <br />
        ( "-" = despesa)</label
      >
      <input type="text" id="amount" placeholder="Inserir valor" v-model="amount" />
    </div>
    <button class="btn">Adicionar</button>
  </form>
</template>

<script setup>
import { useToast } from "vue-toastification";
import { ref } from "vue";

const text = ref("");
const amount = ref("");

// Get toast interface
const toast = useToast();

const emit = defineEmits(["transactionSubmitted"]);

const onSubmit = () => {
  if (!text.value || !amount.value) {
    // Display a toast error message if either field is empty
    toast.error("Os dois campos devem ser preenchidos.");
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit("transactionSubmitted", transactionData);

  // Clear form fields
  text.value = "";
  amount.value = "";
};
</script>
