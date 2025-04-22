<template>
    <div class="register-container">
      <!-- Background Image -->
      <div class="flamingo-bg"></div>
  
      <!-- Register Card -->
      <div class="register-card">
        <div class="register-left">
          <h3 class="title">Welcome to Flamingo Bistrobar!</h3>
          <p>Create a new account to enjoy our services.</p>
        </div>
        <div class="register-right">
          <h3>Register</h3>
          <form @submit.prevent="registerUser">
            <div class="form-group">
              <label for="name">Name</label>
              <input
                type="text"
                id="name"
                v-model="name"
                placeholder="Enter your name"
                required
              />
            </div>
            <div class="form-group">
              <label for="email">Email</label>
              <input
                type="email"
                id="email"
                v-model="email"
                placeholder="Enter your email"
                required
              />
            </div>
            <div class="form-group">
              <label for="password">Password</label>
              <input
                type="password"
                id="password"
                v-model="password"
                placeholder="Enter your password"
                required
              />
            </div>
            <div class="form-group">
              <label for="password_confirmation">Confirm Password</label>
              <input
                type="password"
                id="password_confirmation"
                v-model="password_confirmation"
                placeholder="Confirm your password"
                required
              />
            </div>
            <button type="submit">Register</button>
          </form>
          <div class="login-link">
            <p>Already have an account? <a href="#" @click.prevent="goToLogin">Login here</a></p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        name: '',
        email: '',
        password: '',
        password_confirmation: '',
      };
    },
    methods: {
      async registerUser() {
        try {
          const response = await axios.post('http://127.0.0.1:8000/api/v1/register', {
            name: this.name,
            email: this.email,
            password: this.password,
            password_confirmation: this.password_confirmation,
          });
  
        alert('Registration successful: ' + response.data.user.name);
        this.$router.push('/login'); // Redirect to login page
        } catch (error) {
        if (error.response) {
            // Kiírjuk az error.response.data.errors objektumot, ami az API válaszában található
            const errorMessages = Object.values(error.response.data.errors).join(', ');
            alert('Registration failed: ' + errorMessages); // Validálási hibák kiíratása
        } else {
            alert('An error occurred: ' + error.message);
          }
        }
      },
      goToLogin() {
        this.$router.push('/login'); // Redirect to login page
      },
    },
  };
  </script>
  
  <style scoped>
  .register-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    position: relative;
  }
  
  /* Flamingo Background */
  .flamingo-bg {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 80%;
    height: 80%;
    background-image: url('@/assets/Flamingo_bg.jpg'); /* Használhatod a megfelelő háttérképet */
    background-size: cover;
    background-position: center;
    border-radius: 15px;
    z-index: -1;
  }
  
  /* Register Card */
  .register-card {
    display: flex;
    width: 80%;
    max-width: 700px;
    height: 650px;
    border-radius: 10px;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
    z-index: 1;
  }
  
  .register-left {
    flex: 1;
    background: linear-gradient(to bottom right, rgba(255, 255, 255, 0.7), rgba(255, 255, 255, 0));
    padding: 30px;
    color: #333;
  }
  
  .register-right {
    flex: 1;
    background-color: #343a40;
    padding: 30px;
    color: #fff;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  
  .register-right h3 {
    margin-bottom: 20px;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  input {
    width: 100%;
    padding: 10px;
    border-radius: 5px;
    border: 1px solid #ccc;
    margin-bottom: 10px;
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
  
  .login-link {
    margin-top: 15px;
    text-align: center;
  }
  
  .login-link a {
    color: #ff4081;
    text-decoration: none;
    font-weight: bold;
  }
  
  .login-link a:hover {
    text-decoration: underline;
  }
  </style>
  