<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  total: {
    type: Number,
    required: true,
  },
  budget: {
    type: Number,
    required: true,
  },
  remaining: {
    type: Number,
    required: true,
  },
});
</script>

<template>
  <div>
    <h4>Your Budget</h4>
    <h1 id="budget">{{ budget.toFixed(2) }}</h1>
    <h4>Your Total Expenses</h4>
    <h1 id="total">{{ total.toFixed(2) }}</h1>
    <h4>Remaining Budget</h4>
    <h1 id="remaining">{{ remaining.toFixed(2) }}</h1>
  </div>
</template>