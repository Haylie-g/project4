<script setup>
import { ref, defineEmits } from 'vue';

const name = ref('');
const cost = ref('');

const emit = defineEmits(['grocerySubmitted']);

const onSubmit = () => {
  const groceryData = {
    name: name.value,
    cost: parseFloat(cost.value),
  };

  emit('grocerySubmitted', groceryData);

  name.value = '';
  cost.value = '';
};

</script>


<template>
 <h3>Add a New Grocery</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="name">Enter Grocery Name</label>
      <input type="text" id="name" v-model="name" placeholder="Enter Grocery Name..." />
    </div>

    <div class="form-control">
      <label for="cost">Enter Grocery Cost</label>
      <input type="text" id="cost" v-model="cost" placeholder="Enter Cost" />
    </div>

    <button class="btn">Add Grocery</button>
  </form>


</template>