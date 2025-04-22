<template>
  <div class="admin-dashboard">
    <h2>Admin Dashboard</h2>
    
    <!-- New Dish Form (unchanged) -->
    <h3>Add New Menu Item</h3>
    <form @submit.prevent="addMenuItem">
      <div>
        <label for="name">Dish Name</label>
        <input type="text" v-model="newDish.name" required />
      </div>
      <div>
        <label for="description">Description</label>
        <textarea v-model="newDish.description" required></textarea>
      </div>
      <div>
        <label for="price">Price</label>
        <input type="number" v-model="newDish.price" required />
      </div>
      <div>
        <label for="category">Category</label>
        <select v-model="newDish.category" required>
          <option value="" disabled>Select Category</option>
          <option value="starter">Starter</option>
          <option value="main">Main</option>
          <option value="dessert">Dessert</option>
          <option value="drink">Drink</option>
        </select>
      </div>

      <button type="submit">Add Dish</button>
    </form>

    <!-- Special Offer Form -->
    <h3>Add Special Offer</h3>
    <form @submit.prevent="addSpecialOffer">
      <div>
        <label for="title">Offer Title</label>
        <input type="text" v-model="newOffer.title" required />
      </div>
      <div>
        <label for="image">Offer Image</label>
        <input type="file" @change="handleImageUpload" required />
      </div>
      <button type="submit">Add Special Offer</button>
    </form>

    <!-- Alert if category is invalid -->
    <div v-if="categoryError" class="alert alert-danger">
      <strong>Error!</strong> Invalid category selected. Please choose from "Starter", "Main", "Dessert", or "Drink".
    </div>

    <div v-if="message" class="alert">{{ message }}</div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      newDish: {
        name: "",
        description: "",
        price: "",
        category: "",
      },
      newOffer: {
        title: "",
        image: null,  // For the image upload
      },
      message: "",
      categoryError: false, // Flag for category error
    };
  },
  methods: {
    handleImageUpload(event) {
      this.newOffer.image = event.target.files[0];
    },
    async addMenuItem() {
      const validCategories = ["starter", "main", "dessert", "drink"];
      if (!validCategories.includes(this.newDish.category)) {
        this.categoryError = true;
        return;
      }

      try {
        const response = await axios.post(
          "http://127.0.0.1:8000/api/v1/menus", // API endpoint for adding new menu item
          this.newDish
        );
        this.message = "Menu item added successfully!";
        this.clearForm();
      } catch (error) {
        console.error("Error adding menu item", error);
        this.message = "Failed to add menu item!";
      }
    },
    async addSpecialOffer() {
      const formData = new FormData();
      formData.append('title', this.newOffer.title);
      formData.append('image', this.newOffer.image);

      try {
        const response = await axios.post(
          "http://127.0.0.1:8000/api/v1/special-offers", // API endpoint for adding special offer
          formData,
          { headers: { "Content-Type": "multipart/form-data" } }
        );
        this.message = "Special offer added successfully!";
        this.clearOfferForm();
      } catch (error) {
        console.error("Error adding special offer", error);
        this.message = "Failed to add special offer!";
      }
    },
    clearForm() {
      this.newDish = {
        name: "",
        description: "",
        price: "",
        category: "",
      };
      this.categoryError = false; // Reset category error flag
    },
    clearOfferForm() {
      this.newOffer = {
        title: "",
        image: null,
      };
    },
  },
};
</script>

<style scoped>
.admin-dashboard {
  padding: 20px;
  background-color: #f8f9fa;
  border-radius: 5px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

form div {
  margin-bottom: 15px;
}

input,
textarea,
select {
  width: 100%;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

button {
  padding: 10px;
  background-color: #ff4081;
  border: none;
  border-radius: 5px;
  color: white;
  cursor: pointer;
}

button:hover {
  background-color: #e33873;
}

.alert {
  margin-top: 20px;
  padding: 10px;
  background-color: #d4edda;
  color: #155724;
  border-radius: 5px;
}

.alert-danger {
  background-color: #f8d7da;
  color: #721c24;
}
</style>
