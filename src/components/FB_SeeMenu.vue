<template>
  <div class="see-menu">
    <!-- Special Offer Section -->
    <div v-if="specialOffer" class="special-offer">
      <h3>{{ specialOffer.title }}</h3>
      <img :src="'/storage/' + specialOffer.image_url" alt="Special Offer" class="special-offer-img" />
    </div>

    <h2 class="text-center mb-4">Our Menu</h2>
    <p class="text-center mb-5">Explore our delightful menu of delicious dishes!</p>

    <!-- Menü kategóriák -->
    <div class="menu-category">
      <h3>Starter</h3>
      <div class="menu-grid">
        <div
          v-for="item in filterMenuItems('starter')"
          :key="item.id"
          class="menu-item card shadow-sm"
        >
          <div class="menu-item-content">
            <h3>{{ item.name }}</h3>
            <p>{{ item.description }}</p>
            <div class="price">
              <span>{{ item.price }} FT</span>
            </div>
            <button class="btn btn-primary">Order Now</button>
          </div>
        </div>
      </div>
    </div>

    <div class="menu-category">
      <h3>Main Course</h3>
      <div class="menu-grid">
        <div
          v-for="item in filterMenuItems('main')"
          :key="item.id"
          class="menu-item card shadow-sm"
        >
          <div class="menu-item-content">
            <h3>{{ item.name }}</h3>
            <p>{{ item.description }}</p>
            <div class="price">
              <span>{{ item.price }} FT</span>
            </div>
            <button class="btn btn-primary">Order Now</button>
          </div>
        </div>
      </div>
    </div>

    <div class="menu-category">
      <h3>Dessert</h3>
      <div class="menu-grid">
        <div
          v-for="item in filterMenuItems('dessert')"
          :key="item.id"
          class="menu-item card shadow-sm"
        >
          <div class="menu-item-content">
            <h3>{{ item.name }}</h3>
            <p>{{ item.description }}</p>
            <div class="price">
              <span>{{ item.price }} FT</span>
            </div>
            <button class="btn btn-primary">Order Now</button>
          </div>
        </div>
      </div>
    </div>

    <div class="menu-category">
      <h3>Drinks</h3>
      <div class="menu-grid">
        <div
          v-for="item in filterMenuItems('drink')"
          :key="item.id"
          class="menu-item card shadow-sm"
        >
          <div class="menu-item-content">
            <h3>{{ item.name }}</h3>
            <p>{{ item.description }}</p>
            <div class="price">
              <span>{{ item.price }} FT</span>
            </div>
            <button class="btn btn-primary">Order Now</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      menuItems: [],
      specialOffer: null, // Store special offer data
    };
  },
  mounted() {
    this.fetchMenuItems();
    this.fetchSpecialOffer(); // Fetch special offer on component load
  },
  methods: {
    async fetchMenuItems() {
      try {
        const response = await axios.get("http://127.0.0.1:8000/api/v1/menus");
        this.menuItems = response.data;
      } catch (error) {
        console.error("Error fetching menu items:", error);
      }
    },
    async fetchSpecialOffer() {
      try {
        const response = await axios.get("http://127.0.0.1:8000/api/v1/special-offers"); // Adjust to your API
        this.specialOffer = response.data[0]; // Assuming the first offer is active
      } catch (error) {
        console.error("Error fetching special offer:", error);
      }
    },
    // Filter menu items by category
    filterMenuItems(category) {
      return this.menuItems.filter(item => item.category === category);
    }
  },
};
</script>

<style scoped>
.see-menu {
  background: linear-gradient(to bottom, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
    url('@/assets/Flamingo_int.jpg');
  background-size: cover;
  background-position: 45%;
  background-repeat: no-repeat;
  padding: 50px;
  color: white;
}

h2 {
  font-size: 2.5rem;
  color: #ff4081;
}

p {
  font-size: 1.25rem;
  color: white;
}

.menu-category {
  margin-bottom: 40px;
}

.menu-category h3 {
  font-size: 2rem;
  color: #ff4081;
  margin-bottom: 20px;
  font-weight: bold;
}

.menu-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
}

.menu-item {
  background-color: #fff;
  border-radius: 15px;
  padding: 20px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  overflow: hidden;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.menu-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 25px rgba(0, 0, 0, 0.2);
}

.menu-item-content {
  text-align: center;
}

.menu-item h3 {
  font-size: 1.75rem;
  color: #343a40;
  margin-bottom: 10px;
  font-weight: bold;
}

.menu-item p {
  color: #495057;
  font-size: 1rem;
  margin-bottom: 15px;
}

.price {
  font-size: 1.25rem;
  font-weight: bold;
  margin-bottom: 20px;
  color: #ff4081;
}

button {
  background-color: #ff4081;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 10px 20px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

button:hover {
  background-color: #e33873;
  transform: scale(1.05);
}

.special-offer {
  text-align: center;
  margin-bottom: 40px;
  background-color: rgba(255, 255, 255, 0.8);
  padding: 20px;
  border-radius: 10px;
}

.special-offer-img {
  max-width: 100%;
  height: auto;
  margin-top: 20px;
  border-radius: 10px;
}
</style>
