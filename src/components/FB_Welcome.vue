<script>
export default{
  data(){
    return{

    }
  }
}
</script>

<template >
<!-- Page Content -->
  <div>
  <div class="container mt-5">
      <h2 style="font-size: 2.5rem;" class="text-center mb-4">Welcome to Flamingo Bistrobar</h2>
      <p style="font-size: 1.5rem;" class="text-center">
        Your modern, elegant European bistro experience awaits.
      </p>

      <!-- Carousel or images in a row -->
      <div id="carouselExampleIndicators" class="carousel slide" data-bs-ride="carousel">
        <div class="carousel-inner">
          <div class="carousel-item active">
            <img src="@/assets/slider01.jpg" class="d-block w-100"  alt="Flamingo Bistro Image 1" loading="lazy">
          </div>
          <div class="carousel-item">
            <img src="@/assets/slider02.jpg" class="d-block w-100"  alt="Flamingo Bistro Image 1" loading="lazy">
          </div>
          <div class="carousel-item">
            <img src="@/assets/slider03.jpg" class="d-block w-100"  alt="Flamingo Bistro Image 1" loading="lazy">
          </div>
        </div>
        <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide="prev">
          <span class="carousel-control-prev-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Previous</span>
        </button>
        <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide="next">
          <span class="carousel-control-next-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Next</span>
        </button>
      </div>
    </div>
  </div>
  <br>
  <div class="text-center mt-4">
  <a href="#menu" style="color: #ff4081;" class="btn  btn-dark btn-lg">See the Menu</a>
</div>


    
</template>

<style scoped>
body {
  background-color: #f8f9fa;
}

.carousel-inner img {
  height: 500px; /* Adjust height as needed */
  object-fit: cover;
}

h2 {
  color: #ff4081; /* Elegant pink color, similar to flamingos */
}

p {
  font-size: 1.2rem;
  color: #333333;
}

.carousel-control-prev-icon, .carousel-control-next-icon {
  background-color: #ff4081; /* Flamingo pink */
}

.hover-effect:hover {
  background-color: #ff4081; /* Flamingo pink */
  color: white;
}
.carousel-control-prev-icon, .carousel-control-next-icon {
  background-color: #ff4081; /* Flamingo pink */
  border-radius: 50%;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
}
.carousel-inner img {
  border: 4px solid white; /* Fehér szegély */
  border-radius: 12px; /* Lekerekített sarkok */
  transition: transform 0.3s ease, box-shadow 0.3s ease; /* Zökkenőmentes animáció */
}
.carousel-inner img:hover {
  transform: scale(1.05); /* Nagyobb kép hover hatás */
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2); /* Erősebb árnyék hover hatás */
}
.carousel-inner img {
  transition: transform 0.3s ease;
}
.carousel-inner img:hover {
  transform: scale(1.05); /* Kép nagyítása hover hatásra */
}


</style>
