<template>
  <div id="app">
    <h1>Gestion des Fournitures</h1>

    <!-- Supply Form -->
    <SupplyForm
      :initialData="currentSupply"
      :isEditing="isEditing"
      @submit="handleFormSubmit"
    />

    <!-- Supply List -->
    <SupplyList
      :supplies="supplies"
      @edit-supply="editSupply"
      @remove-supply="removeSupply"
    />
  </div>
</template>

<script>
import SupplyForm from './components/SupplyForm.vue';
import SupplyList from './components/SupplyList.vue';

export default {
  name: 'App',
  components: {
    SupplyForm,
    SupplyList
  },
  data() {
    return {
      supplies: [],
      currentSupply: { name: '', quantity: 0, supplier: '' },
      isEditing: false
    };
  },
  methods: {
    handleFormSubmit(newSupply) {
      if (!newSupply.name || !newSupply.supplier || newSupply.quantity <= 0) {
        return; // Prevent adding an empty or invalid supply
      }

      if (this.isEditing) {
        // Update the supply in the list
        const index = this.supplies.findIndex(s => s.name === this.currentSupply.name);

        if (index !== -1) {
          this.supplies[index] = { ...newSupply }; // Replace old with new
        }
      } else {
        // Add new supply
        this.supplies.push({ ...newSupply });
      }

      // Reset the form after submitting
      this.resetForm();
    },

    editSupply(supply) {
      this.currentSupply = { ...supply };
      this.isEditing = true;
    },

    removeSupply(index) {
      this.supplies.splice(index, 1);
    },

    resetForm() {
      this.currentSupply = { name: '', quantity: 0, supplier: '' };
      this.isEditing = false;
    }
  }
};
</script>

<style scoped>
/* Your styles here */
</style>
