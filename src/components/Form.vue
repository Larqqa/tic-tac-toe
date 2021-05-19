<template>
  <div>
    <p v-if="errors.length">
      <b>Please correct the following error(s):</b>
      <ul>
        <li v-for="(error, i) in errors" :key="i">{{ error }}</li>
      </ul>
    </p>

    <form @submit="checkForm">
      <label for="name">Name:</label>
      <input
        id="name"
        type="text"
        v-model.lazy="name"
        required
        placeholder="Product name"
      />

      <label for="amount">Amount:</label>
      <input
        id="amount"
        type="number"
        v-model.number="amount"
        min="1"
      />

      <button type="submit">Add item</button>
      <button type="button" v-show="hasItems" @click="$emit('emptyList')" style="width: max-content">Clear list</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Form',
  props: {
    hasItems: Boolean
  },
  data() {
    return {
      name: '',
      amount: 1,
      errors:[],
    }
  },
  emits: [
    'formData',
    'emptyList'
  ],
  methods: {
    generateId: function() {
      return ([1e7]+-1e3+-4e3+-8e3+-1e11).replace(/[018]/g, c =>
        (c ^ crypto.getRandomValues(new Uint8Array(1))[0] & 15 >> c / 4).toString(16)
      );
    },
    checkForm: function(e) {
      e.preventDefault();
      this.errors = [];

      if (this.name && this.amount) {
        this.$emit('formData', {
          id: this.generateId(),
          name: this.name,
          amount: this.amount,
        });

        this.name = '';
        this.amount = 1;
        return;
      }

      if (!this.name) {
        this.errors.push('Name required!');
      }

      if (isNaN(this.amount)) {
        this.errors.push('Amount required!');
      } else if (this.amount < 1) {
        this.errors.push('Amount is lower than 1!');
      }
    }
  }
}
</script>

<style scoped>
  form {
    display: grid;
    grid-template-columns: max-content auto;
    width: 200px;
    row-gap: 1rem;
    column-gap: 1rem;
  }
</style>