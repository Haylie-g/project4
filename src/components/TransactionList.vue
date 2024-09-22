<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  groceries: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(['groceryDeleted']);

const deleteGrocery = (id) => {
  emit('groceryDeleted', id);
};
</script>

<template>
  <h3>Grocery List</h3>
  <ul id="list" class="list">
    <li
      v-for="grocery in groceries"
      v-bind:key="grocery.id"
      v-bind:class="grocery.cost < 0 ? 'minus' : 'plus'"
    >
      {{ grocery.name }} <span>${{ grocery.cost.toFixed(2) }}</span>
      <button @click="deleteGrocery(grocery.id)" class="delete-btn">x</button>
    </li>
  </ul>
</template>