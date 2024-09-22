<script setup>
import Header from './components/Header.vue';
import AddGrocery from './components/AddGrocery.vue';
import Balance from './components/Balance.vue';

import { ref, computed } from 'vue';
const groceries = ref([]);
const budget = ref(150);

const totalCost = computed(() => {
  return groceries.value.reduce((acc, item) => {
    return acc + item.cost;
  }, 0);
});

const remainingBudget = computed(() => {
  return budget.value - totalCost.value;
});

const handleGrocery = (groceryData) => {
  groceries.value.push({
    id: generateID(),
    name: groceryData.name,
    cost: groceryData.cost,
  });
};

const generateID = () => {
  return Math.floor(Math.random() * 10000000);
};


</script>

<template>
  <Header></Header>
  <AddGrocery></AddGrocery>
  <Balance :total="totalCost" :budget="budget" :remaining="remainingBudget" />

</template>

