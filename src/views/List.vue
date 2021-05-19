<template>
  <div>
    <h1>Shopping list</h1>

    <button @click="showForm = !showForm" class="show-form">{{showForm ? 'Cancel' : 'Add entry'}}</button>
    <Form
      v-show="showForm"
      @formData="handleInput"
      @emptyList="emptyList"
      :hasItems="products.length > 0"
    />
    <hr>

    <div class="products">
      <Product
        v-for="product in products"
        :key="product.id"
        :id="product.id"
        :name="product.name"
        :amount="product.amount"
        @decrementItem="decrementItem"
        @incrementItem="incrementItem"
        @removeItem="removeItem"
      />
    </div>
  </div>
</template>

<script>
  import Form from '../components/Form.vue';
  import Product from '../components/Product.vue';

  export default {
    name: 'List',
    components: {
      Form,
      Product
    },
    data() {
      return {
        products: [
          {id: "ed19acf3-0a7f-4f1d-8464-b2649e854ec1", name: "ice cream", amount: 1},
          {id: "7877d9b3-1c12-4a86-baf2-d629385c1570", name: "coka cola", amount: 1}
        ],
        showForm: false
      }
    },
    methods: {
      handleInput: function(input) {
        const existingObject = this.products.findIndex(product => product.name === input.name);

        if (existingObject >= 0) {
          this.products[existingObject].amount += input.amount;
        } else {
          this.products = [ ...this.products, input ];
        }
      },
      emptyList: function() {
        if (confirm("Are you sure you want to empty this list?"))
          this.products = [];
      },
      decrementItem: function(id) {
        const existingObject = this.products.findIndex(product => product.id === id);
        if (existingObject >= 0)
          if (this.products[existingObject].amount > 1)
            this.products[existingObject].amount--;
      },
      incrementItem: function(id) {
        const existingObject = this.products.findIndex(product => product.id === id);
        if (existingObject >= 0)
          this.products[existingObject].amount++;
      },
      removeItem: function(id) {
        if (confirm("Are you sure you want to remove this product?"))
          this.products = this.products.filter(product => product.id !== id);
      }
    }
  }
</script>

<style scoped>
  button {
    display: block;
  }

  .show-form {
    margin-bottom: 1rem;
  }

  .products {
    display: grid;
    grid-template-columns: max-content max-content max-content max-content max-content;
    row-gap: 1rem;

    align-items: center;
  }
</style>