<script setup>
import Header from './components/Header.vue';
import AddGrocery from './components/AddGrocery.vue';
import Balance from './components/Balance.vue';
import GroceryList from './components/GroceryList.vue';
import TransactionList from './components/TransactionList.vue';

import { ref, computed, onMounted} from 'vue';
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
    cost: parseFloat(groceryData.cost),
  });
  saveToLocalStorage();
};

const handleDeleteGrocery = (id) => {
  groceries.value = groceries.value.filter(grocery => grocery.id !== id);
  saveToLocalStorage(); // Update local storage
};

const generateID = () => {
  return Math.floor(Math.random() * 10000000);
};

const saveToLocalStorage = () => {
  localStorage.setItem('groceries', JSON.stringify(groceries.value));
};

onMounted(() => {
  const savedGroceries = JSON.parse(localStorage.getItem('groceries'));
  if (savedGroceries) {
    groceries.value = savedGroceries;
  }
});


</script>

<template>
  <Header></Header>
  <AddGrocery @grocerySubmitted="handleGrocery" />
  <Balance :total="totalCost" :budget="budget" :remaining="remainingBudget" />
  <TransactionList :groceries="groceries" @groceryDeleted="handleDeleteGrocery" />

</template>

