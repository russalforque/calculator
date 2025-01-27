<template>
  <div >
    <!-- Navbar -->
    <nav class="p-10">
      <div class="container mx-auto flex justify-between items-center">
        <h1 class="text-dark text-xl font">russ<span>.</span></h1>
        <ul class="flex space-x-6 text-dark">
          <li><a href="#home" class="hover:text-dark-400">Home</a></li>
          <li><a href="#features" class="hover:text-dark-400">Features</a></li>
          <li><a href="#contact" class="hover:text-dark-400">Contact</a></li>
        </ul>
      </div>
    </nav>

    <section id="home" class="bg-[#fff]  h-screen flex items-center justify-center">
      <div class="text-center intro">
        <h2 class="text-5xl font-bold">Welcome to Our Website</h2>
        <p class="text-lg mb-6">Lorem ipsum dolor, sit amet consectetur adipisicing elit. Sapiente tenetur necessitatibus expedita voluptates, ab molestiae incidunt, dolore ullam neque aliquid possimus porro harum sint corporis at! Maxime doloremque non velit.</p>
        <button class="bg-yellow-500 text-black px-6 py-3 rounded-lg hover:bg-yellow-400 transition duration-300">Get Started</button>
      </div>
    </section>

    <!-- Features Section -->
    <section id="features" class="py-16">
      <div class="container mx-auto text-center">
        <h3 class="text-4xl font-semibold mb-8">Our Features</h3>
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
          <div class="bg-white p-6 rounded-lg shadow-lg">
    <!-- 3D Image Effect -->
    <img
      src="./assets/settings.png"
      alt="Feature Image"
      class="transition-transform transform hover:scale-105 hover:rotate-3d hover:shadow-xl rounded-lg"
    />
    <h4 class="text-xl font-semibold mb-4">Feature 1</h4>
    <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Odit consequatur rerum unde porro, officiis beatae libero nihil quod ad possimus et nobis eum voluptatem iusto in ipsam saepe inventore dicta.</p>
  </div>
          <div class="bg-white p-6 rounded-lg shadow-lg">
            <img src="./assets/settings.png">
            <h4 class="text-xl font-semibold mb-4">Feature 2</h4>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Tempora assumenda accusamus doloribus aspernatur aliquid optio ea mollitia, vitae maiores sed voluptates dolorum, voluptatem similique praesentium debitis sunt expedita excepturi autem.</p>
          </div>
          <div class="bg-white p-6 rounded-lg shadow-lg">
            <img src="./assets/settings.png">
            <h4 class="text-xl font-semibold mb-4">Feature 3</h4>
            <p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Numquam, deserunt quos quae omnis molestias a ipsam doloremque officiis doloribus quisquam cupiditate assumenda culpa optio, voluptatibus incidunt nisi deleniti. Tempore, obcaecati!</p>
          </div>
        </div>
      </div>
    </section>


    <section id="about" class=""> 
      <div class="flex text-center aboutText">
        <div class="basis-2/3">
          <h1>Lorem</h1>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Explicabo voluptatum, ratione fuga corrupti incidunt iure pariatur enim repellendus perferendis dolores, aliquid animi quae in reprehenderit aliquam nisi, minima distinctio qui!</p>
        </div>
        <div class="basis-1/3">
          <img src="">
        </div>
      </div>

    </section>

    <!-- Contact Section -->
    <section id="contact" class="py-16 text-dark">
      <div class="container mx-auto text-center">
        <h3 class="text-4xl font-semibold mb-8">Contact Us</h3>
        <p class="text-lg mb-6">Have any questions? We're here to help. Get in touch with us!</p>
        <button class="bg-yellow-500 text-black px-6 py-3 rounded-lg hover:bg-yellow-400 transition duration-300">Contact</button>
      </div>
    </section>
    

    <!-- Footer -->
    <footer class="bg-gray-800 text-white py-4 text-center">
      <p>&copy; 2025 russ. All rights reserved.</p>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style scoped>

nav {
  -webkit-box-shadow: 0px 5px 76px 4px rgba(189,189,189,1);
-moz-box-shadow: 0px 5px 76px 4px rgba(189,189,189,1);
box-shadow: 0px 5px 76px 4px rgba(189,189,189,1);
}

ul li a{
  margin: 20px;
}

.font {
  font-weight: bolder;
}
.intro h2 {
  font-weight: bold;
}
.intro p{
  margin-top: 10px;
}

.intro button{
  margin-top: 20px;
}
img {
  width: 500px;
}

img:hover {
  transform: perspective(600px) rotateY(10deg) rotateX(10deg);
  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1), 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease-in-out;
}

.aboutText h1 {
  font-size: 40px;
  font-weight: bold;
}
.aboutText p {
  font-size: 18px;
}

#contact, #about {
  margin-top: 200px;
}

</style>
