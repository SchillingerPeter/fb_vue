<script>
import axios from 'axios';

export default {
  data() {
    return {
      email: '',
      password: '',
    };
  },
  methods: {
    async loginUser() {
      try {
        const response = await axios.post('http://127.0.0.1:8000/api/v1/login', {
          email: this.email,
          password: this.password,
        });

        // Handle successful login (e.g., store token or navigate)
        alert('Login successful: ' + response.data.message);  // Display successful login message

        // You can also store the token and user info here if needed
        localStorage.setItem('token', response.data.token);
        localStorage.setItem('user', JSON.stringify(response.data.user));

        // Admin check and redirection
        if (response.data.user.role === 'admin') {
          this.$parent.showAdminPage();  // Pass the logic to App.vue for redirecting to admin
        }
      } catch (error) {
        // Handle errors (invalid credentials, etc.)
        if (error.response) {
          alert('Login failed: ' + error.response.data.message);  // Display login error
        } else {
          alert('An error occurred: ' + error.message); // If no response, show the error message
        }
      }
    },
    goToRegister() {
      // Redirect to the register page
      console.log('Redirecting to registration page');
      this.$parent.showRegisterPage(); // Call the showRegisterPage method from App.vue
    },
  },
};
</script>


<template>
  <div class="login-container">
    <!-- Background Image -->
    <div class="flamingo-bg"></div>

    <!-- Login Card -->
    <div class="login-card">
      <div class="login-left">
        <h3 class="title">Welcome Back!</h3>
        <p>Please login to your account</p>
      </div>
      <div class="login-right">
        <h3>Login</h3>
        <form @submit.prevent="loginUser">
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
          <button type="submit">Login</button>
        </form>

        <!-- Az új mező és link hozzáadása -->
        <div class="register-link">
          <p>Don't have an account? <a href="#" @click.prevent="goToRegister">Register here</a></p>
        </div>
      </div>
    </div>
  </div>
</template>



<style scoped>
.login-container {
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
  background-image: url('@/assets/Flamingo_bg.jpg');
  background-size: cover;
  background-position: center;
  border-radius: 15px;
  z-index: -1;
}

/* Login Card */
.login-card {
  display: flex;
  width: 80%;
  max-width: 700px;
  height: 480px;
  border-radius: 10px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
  z-index: 1;
}

.login-left {
  flex: 1;
  background: linear-gradient(to bottom right, rgba(255, 255, 255, 0.7), rgba(255, 255, 255, 0));
  padding: 30px;
  color: #333;
}

.login-right {
  flex: 1;
  background-color: #343a40;
  padding: 30px;
  color: #fff;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.login-right h3 {
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

/* Register link */
.register-link {
  margin-top: 15px;
  text-align: center;
}

.register-link a {
  color: #ff4081;
  text-decoration: none;
  font-weight: bold;
}

.register-link a:hover {
  text-decoration: underline;
}
</style>