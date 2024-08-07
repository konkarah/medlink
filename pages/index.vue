<template>
  <nav class="bg-gray-800 text-white p-4">
    <div class="container mx-auto flex justify-between items-center">
      <div class="text-lg font-semibold">My Website</div>
      <div>
        <a href="#" class="hover:text-gray-400 px-4">Home</a>
        <a href="#" class="hover:text-gray-400 px-4">About</a>
        <a href="#" class="hover:text-gray-400 px-4">Services</a>
        <a href="#" class="hover:text-gray-400 px-4">Contact</a>
      </div>
    </div>
  </nav>
<div class="grid grid-cols-2"> 
  
  <div class="mybg flex items-center ">
    <h2  class="font-bold text-4xl p-4 text-gray-800">Managing of profitable health
      services through the use of innovative human and technological resources,</h2>
  </div>
  <div>
    <img src="~/assets/images/bg1.jpeg" alt="">
  </div>
</div>
<div class="services-section p-4">
  <h2 class="text-2xl font-semibold mb-4">Our Services</h2>
  <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
    <Card v-for="service in services" :key="service.title" class="p-4 shadow-lg">
      <template #header>
        <div class="relative">
          <img :src="service.image" alt="" class="w-full h-32 object-cover rounded-t-md" />
          <h3 class="text-xl font-semibold absolute bottom-2 left-2 text-white bg-black bg-opacity-50 p-2 rounded">
            {{ service.title }}
          </h3>
        </div>
      </template>
      <p class="mt-4 text-gray-700">{{ service.description }}</p>
      <Button label="Learn More" class="mt-2" />
    </Card>
  </div>
</div>
<div>
  <div class="grid grid-cols-2 ">
    <img src="" alt=""  class="bg-auto bg-no-repeat bg-center ">
  </div>
  <div>

  </div>
</div>
</template>

<script setup>
const services = [
  { 
    title: 'Service 1', 
    description: 'Description for service 1', 
    image: '/images/service1.jpg' // Update with the correct path to your image
  },
  { 
    title: 'Service 2', 
    description: 'Description for service 2', 
    image: '/images/service2.jpg' // Update with the correct path to your image
  },
  { 
    title: 'Service 3', 
    description: 'Description for service 3', 
    image: '/images/service3.jpg' // Update with the correct path to your image
  },
  // Add more services as needed
];
</script>
<style>
.mybg{
background-color: rgb(247,247,247);
}
.services-section {
  background-color: #f9f9f9;
}
.card img {
  border-radius: 0.5rem 0.5rem 0 0;
}
.card-header {
  position: relative;
}
.card-header img {
  border-radius: 0.5rem 0.5rem 0 0;
}
.card-header h3 {
  position: absolute;
  bottom: 1rem;
  left: 1rem;
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  padding: 0.5rem;
  border-radius: 0.25rem;
}
</style>