<script setup>
  import { defineProps } from "vue";

  const props = defineProps({
    transactions: {
      type: Array,
      required: true
    }
  })

  const emit = defineEmits(["transactionDeleted"]);
 
  const handleDelete = (id) => {
    emit("transactionDeleted",id);
  }
</script>

<template>
  <h3>Transactions History</h3>

  <div v-if="transactions.length > 0">
    <ul id="list" class="list">
      <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount < 0 ? 'minus' : 'plus' ">
        {{transaction.text}}
        <span>$ {{transaction.amount.toFixed(2)}}</span>
        <button @click="handleDelete(transaction.id)" class="delete-btn">X</button>
      </li>
    </ul>
  </div>

  <p v-else>Oops, no transactions to display</p>

</template>