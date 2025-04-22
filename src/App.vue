<script>
import FB_Register from "./components/FB_Register.vue";
import FB_Login from "./components/FB_Login.vue";
import FB_Welcome from "./components/FB_Welcome.vue";
import FB_AdminDash from "./components/FB_AdminDash.vue";
import FB_SeeMenu from "./components/FB_SeeMenu.vue";
export default{
  data(){
    return{
      currentPage: "welcome", // Default page is Welcome  
    }
  },
  components:{
    FB_Welcome,
    FB_Login,
    FB_Register,
    FB_AdminDash,
    FB_SeeMenu,
  },
  methods:{
    showWelcomePage() {
      this.currentPage = "welcome"; // Set to 'welcome' page
    },
    showLoginPage() {
      this.currentPage = "login"; // Set to 'login' page
    },
    showRegisterPage() {
      this.currentPage = "register"; // Regisztrációs oldal
    },
    showAdminPage() {
      this.currentPage = 'admin'; // Show the Admin page
    },
    showAdminPage() {
      this.currentPage = 'admin'; // Show the Admin page
    },
    showMenuPage() {
      this.currentPage = "menu";  // Átváltás Menu oldalra
    },
  }

}
</script>

<template>
 <!-- Navbar -->
 <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">
        <img src="@/assets/Flamingo_logo.png" style="width: 100px;"  alt="" />
        <a style="font-size: 1.4rem;" class="navbar-brand" href="#">Flamingo Bistrobar</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item">
              <a class="nav-link text-light p-2 px-4 rounded hover-effect" href="#" @click.prevent="showWelcomePage">Home</a> <!-- Welcome link -->
            </li>
            <li class="nav-item">
              <a class="nav-link text-light p-2 px-4 rounded hover-effect" href="#" @click.prevent="showLoginPage">Login</a> <!-- Login link -->
            </li>
            <li class="nav-item">
              <a class="nav-link text-light p-2 px-4 rounded hover-effect" href="#" @click.prevent="showMenuPage">Menu</a>
            </li>
            <li class="nav-item">
              <a class="nav-link text-light p-2 px-4 rounded hover-effect" href="#">About</a>
            </li>
            <li class="nav-item">
              <a class="nav-link text-light p-2 px-4 rounded hover-effect" href="#">Contact</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <FB_Welcome v-if="currentPage === 'welcome'" /> <!-- Show Welcome component -->
    <FB_Login v-if="currentPage === 'login'" />    <!-- Show Login component -->
    <FB_Register v-if="currentPage === 'register'" /> <!-- Show Register component -->
    <FB_AdminDash v-if="currentPage === 'admin'" /> 
    <FB_SeeMenu v-if="currentPage === 'menu'" />  

  


</template>

<style scoped>
.navbar {
  background-color: #333333;
}
.navbar .nav-link {
  color: #000000; /* Alapértelmezett szín a gombokhoz (például fekete) */
  transition: color 0.3s ease; /* Zökkenőmentes színváltozás */
}

.navbar .nav-link:hover {
  color: #ff4081; /* Hover szín (pl. flamingó pink) */
  text-decoration: underline; /* Aláhúzott stílus a hover állapotban (opcionális) */
}
.hover-effect:hover {
  background-color: #ff4081; /* Flamingo pink */
  color: white;
}

</style>
