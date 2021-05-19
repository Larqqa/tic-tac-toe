<template>
  <input class="product--check" type="checkbox">
  <p class="product--name">{{name}}</p>

  <button v-show="amount <= 1" class="product--remove product--button" @click="$emit('removeItem', id)">
    <span class="material-icons">delete</span>
  </button>
  <button v-show="amount > 1" class="product--increment product--button" @click="$emit('decrementItem', id)">
    <span class="material-icons">remove</span>
  </button>

  <p class="product--amount">{{amount}}</p>

  <button class="product--button product--decrement" @click="$emit('incrementItem', id)">
    <span class="material-icons">add</span>
  </button>
</template>

<script>
  export default {
    name: 'Product',
    props: {
      id: String,
      name: String,
      amount: Number,
    },
    emits: [
      'incrementItem',
      'decrementItem',
      'removeItem'
    ]
  }
</script>

<style scoped>
  .product--name,
  .product--amount {
    margin: .5rem 1rem;
    margin-right: 0;
  }

  .product--button {
    margin: 0;
    margin-left: 1rem;
  }

  .product--check {
    margin: 0;
  }
</style>