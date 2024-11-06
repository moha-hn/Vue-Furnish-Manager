<template>
    <div class="supply-list">
      <h2>Liste des Fournitures</h2>
      <div v-if="supplies.length === 0" class="no-supplies">
        <p>Aucune fourniture à afficher.</p>
      </div>
      <ul>
        <li v-for="(supply, index) in supplies" :key="index" class="supply-item">
          <div class="supply-details">
            <p><strong>Nom:</strong> {{ supply.name }}</p>
            <p><strong>Quantité:</strong> {{ supply.quantity }}</p>
            <p><strong>Fournisseur:</strong> {{ supply.supplier }}</p>
          </div>
          <button @click="editSupply(supply)" class="edit-btn">Modifier</button>
          <button @click="removeSupply(index)" class="remove-btn">Supprimer</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: ['supplies'],
    methods: {
      editSupply(supply) {
        // Emit the selected supply for editing
        this.$emit('edit-supply', supply);
      },
      removeSupply(index) {
        // Emit the index of the supply to be removed
        this.$emit('remove-supply', index);
      }
    }
  };
  </script>
  
  <style scoped>
  .supply-list {
    max-width: 600px;
    margin: 20px auto;
    padding: 20px;
    background-color: #1b1b1b; /* Dark background for Green Lantern theme */
    color: #e0e0e0; /* Light text color for readability */
    border-radius: 5px;
  }
  
  h2 {
    text-align: center;
    margin-bottom: 20px;
  }
  
  .no-supplies {
    text-align: center;
    font-size: 18px;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  .supply-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px;
    border-bottom: 1px solid #333;
  }
  
  .supply-details {
    flex-grow: 1;
  }
  
  button {
    padding: 8px 15px;
    font-size: 16px;
    color: #fff;
    background-color: #66bb6a; /* Green button background */
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
    margin-left: 10px;
  }
  
  button:hover {
    background-color: #4caf50; /* Slightly darker green on hover */
  }
  
  button.remove-btn {
    background-color: #e53935; /* Red button for remove */
  }
  
  button.remove-btn:hover {
    background-color: #d32f2f; /* Slightly darker red on hover */
  }
  </style>
  