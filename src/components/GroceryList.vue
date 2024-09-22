<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  groceries: {
    type: Array,
    required: true,
  },
});
</script>

<template>
  <div class="grocery-list-container">
    <h3>Grocery List</h3>
    <ul>
      <li v-for="grocery in groceries" :key="grocery.id">
        <span>{{ grocery.name }}</span> - <span>${{ grocery.cost.toFixed(2) }}</span>
      </li>
    </ul>
  </div>
</template>