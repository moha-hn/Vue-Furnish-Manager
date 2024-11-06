<template>
    <form @submit.prevent="handleSubmit">
      <input v-model="supply.name" placeholder="Nom fourniture" required />
      <input v-model.number="supply.quantity" type="prix" placeholder="" required />
      <input v-model="supply.supplier" placeholder="Fournisseur" required />
      <button type="submit">{{ isEditing ? "modifier" : "ajouter" }} fourniture</button>
    </form>
  </template>
  
  <script>
  export default {
    props: ['initialData', 'isEditing'],
    data() {
      return {
        supply: this.initialData || { name: '', quantity: 0, supplier: '' }
      };
    },
    methods: {
      handleSubmit() {
        this.$emit('submit', { ...this.supply });
        this.supply = { name: '', quantity: 0, supplier: '' }; // reset form
      }
    },
    watch: {
      initialData(newData) {
        this.supply = newData;
      }
    }
  };
  </script>
  
 <style scoped>
  /* Form container styling */
  form {
    display: flex;
    flex-direction: column;
    gap: 15px;
    max-width: 400px;
    margin: 20px auto;
    padding: 20px;
    border: 1px solid #2e7d32;
    border-radius: 5px;
    background-color: #1b1b1b; /* Dark background for Green Lantern theme */
    color: #e0e0e0; /* Light text color for readability */
  }

  /* Input fields styling */
  input {
    padding: 12px;
    font-size: 18px;
    color: #e0e0e0; /* Light text */
    background-color: #333; /* Darker background for input fields */
    border: 1px solid #2e7d32;
    border-radius: 4px;
    transition: border-color 0.3s ease, background-color 0.3s ease;
  }

  /* Input fields on focus (active) */
  input:focus {
    outline: none;
    border-color: #66bb6a; /* Green highlight when active */
    background-color: #2b2b2b;
  }

  /* Button styling */
  button {
    padding: 12px;
    font-size: 18px;
    color: #1b1b1b; /* Dark text for contrast */
    background-color: #66bb6a; /* Green button background */
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  /* Button hover effect */
  button:hover {
    background-color: #4caf50; /* Slightly darker green on hover */
  }

  /* Placeholder styling */
  input::placeholder {
    color: #888; /* Gray for placeholder text */
  }
</style>


  