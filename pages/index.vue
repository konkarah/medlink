<template>
  <div>
    <nav class="mycol text-white p-4">
      <div class="container mx-auto flex flex-wrap items-center justify-between">
        <!-- Logo or Website Title -->
        <div class="flex items-center">
          <img src="/assets/images/med-link.svg" alt="logo" class="h-10"> <!-- Adjust the height as needed -->
        </div>
        
  
        <!-- Mobile Menu Button -->
        <button @click="toggleMenu" class="text-white block md:hidden focus:outline-none">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
          </svg>
        </button>
  
        <!-- Menu Items -->
        <div :class="{'block': isMenuOpen, 'hidden': !isMenuOpen}" class="w-full md:flex md:w-auto">
          <div class="flex flex-col md:flex-row md:space-x-4 mt-4 md:mt-0">
            <a href="#" class="block px-4 py-2 text-white hover:text-gray-400">Home</a>
            <a href="#" class="block px-4 py-2 text-white hover:text-gray-400">About</a>
            <a href="#" class="block px-4 py-2 text-white hover:text-gray-400">Services</a>
            <a href="#" class="block px-4 py-2 text-white hover:text-gray-400">Contact</a>
          </div>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <div class="mybg grid grid-cols-1 md:grid-cols-2 gap-4 p-6">
      <div class="flex items-center justify-center p-4 ">
        <h2 class="font-bold text-2xl md:text-4xl text-gray-800 text-center md:text-left">
          Managing of profitable health services through the use of innovative human and technological resources
        </h2>
      </div>
      <div class="flex items-center justify-center">
        <img src="~/assets/images/bg1.jpeg" alt="Background Image" class="w-full h-auto rounded-md" />
      </div>
    </div>

    <div class="services-section p-6 bg-gray-100">
      <h2 class="text-3xl font-semibold mb-6 text-center text-gray-800">Our Services</h2>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <Card v-for="(service, index) in services" :key="index" class="shadow-lg rounded-lg overflow-hidden bg-white">
          <template #header>
            <div class="relative">
              <img :src="service.image" alt="Service image" class="w-full h-40 object-cover" />
              <h3 class="absolute bottom-0 left-0 text-xl font-semibold text-white bg-black bg-opacity-60 p-3 rounded-t-lg">
                {{ service.title }}
              </h3>
            </div>
          </template>
          <template #content>
            <p class="p-4 text-gray-700">
              {{ service.description }}
            </p>
          </template>
          <template #footer>
            <div class="flex justify-center p-4">
              <button @click="openModal(service)"  class="mycol text-white p-2 rounded-md" >Learn More</button>
            </div>
          </template>
        </Card>
      </div>
      
      <!-- PrimeVue Dialog Component -->
      <Dialog v-model:visible="modalVisible" header="Service Details" :style="{ width: '80vw', maxWidth: '600px' }" modal>
        <img :src="selectedService?.image" alt="Service image" class="w-full h-40 object-cover mb-4" />
        <h3 class="text-xl font-semibold mb-2">{{ selectedService?.title }}</h3>
        <h4 class="text-lg mb-4">{{ selectedService?.subtitle }}</h4>
        <p class="text-gray-700 mb-4">{{ selectedService?.description }}</p>
        <button icon="pi pi-times" @click="closeModal" class="mycol text-white p-2 rounded-md" >Close</button>
      </Dialog>
    </div>

    <!-- Feature Section -->
    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 p-8 bg-white rounded-md">
      <div class="flex items-center justify-center">
        <img src="https://images.pexels.com/photos/305565/pexels-photo-305565.jpeg" alt="Feature Image" class="w-full h-auto rounded-md" />
      </div>
      <div class="flex items-center p-4">
        <p class="text-gray-800">
          Guaranteeing the attention, security, and trust of the patients, respecting their life regardless of their national origin.
          Additionally, assuring ethical and honest practices, respecting all the existing regulations in each country where we have a presence through teamwork,
          maximizing the value of health care, laboratories supply and management, and equipment resources.
        </p>
      </div>
    </div>

    <!-- Testimonials Section -->
    <div class="testimonials-section p-6 bg-gray-50">
      <h2 class="text-3xl font-semibold mb-6 text-center text-gray-800">What Our Clients Say</h2>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <div v-for="testimonial in testimonials" :key="testimonial.name" class="bg-white p-6 rounded-lg shadow-md flex flex-col items-center text-center">
          <img :src="testimonial.image" alt="Testimonial image" class="w-24 h-24 rounded-full object-cover mb-4 border-2 border-gray-200" />
          <p class="text-gray-600 italic mb-4">
            "{{ testimonial.quote }}"
          </p>
          <div class="font-semibold text-gray-800">{{ testimonial.name }}</div>
          <div class="text-gray-500">{{ testimonial.role }}</div>
        </div>
      </div>
    </div>

    <!-- Contact Form Section -->
    <div class="contact-form-section p-6 bg-gray-50">
      <h2 class="text-3xl font-semibold mb-6 text-center text-gray-800">Contact Us</h2>
      <form @submit.prevent="handleSubmit" class="max-w-md mx-auto bg-white p-8 rounded-lg shadow-md">
        <div class="mb-4">
          <label for="name" class="block text-gray-700 text-sm font-bold mb-2">Name</label>
          <input
            type="text"
            id="name"
            v-model="form.name"
            required
            class="w-full px-3 py-2 border border-gray-300 rounded-md"
            placeholder="Your Name"
          />
        </div>
        <div class="mb-4">
          <label for="email" class="block text-gray-700 text-sm font-bold mb-2">Email</label>
          <input
            type="email"
            id="email"
            v-model="form.email"
            required
            class="w-full px-3 py-2 border border-gray-300 rounded-md"
            placeholder="Your Email"
          />
        </div>
        <div class="mb-4">
          <label for="message" class="block text-gray-700 text-sm font-bold mb-2">Message</label>
          <textarea
            id="message"
            v-model="form.message"
            required
            rows="4"
            class="w-full px-3 py-2 border border-gray-300 rounded-md"
            placeholder="Your Message"
          ></textarea>
        </div>
        <div class="flex items-center justify-between">
          <button
            type="submit"
            class="mycol text-white font-bold py-2 px-4 rounded hover:bg-blue-600 focus:outline-none focus:shadow-outline"
          >
            Send
          </button>
          <p v-if="successMessage" class="text-green-500">{{ successMessage }}</p>
          <p v-if="errorMessage" class="text-red-500">{{ errorMessage }}</p>
        </div>
      </form>
    </div>

    <!-- Footer -->
    <footer class="mycol text-white p-4 flex justify-center">
      <div class="container mx-auto flex flex-wrap flex-col md:flex-row justify-between items-center">
        <!-- Existing section: Footer text and links -->
        <div class="text-center md:text-left mb-4 md:mb-0">
          <p class="text-sm mb-2">&copy; 2024 Zemy-Group.com. All rights reserved.</p>
          <p class="text-sm">
            <a href="#" class="hover:text-gray-400">Privacy Policy</a> | 
            <a href="#" class="hover:text-gray-400">Terms of Service</a>
          </p>
        </div>
        
        <!-- New section: Get in Touch -->
        <div class="text-center md:text-left mb-4 md:mb-0">
          <h4 class="text-lg font-semibold mb-2">Get in Touch</h4>
          <p class="text-sm mb-2">147 W 35th St, New York, NY 10001</p>
          <p class="text-sm mb-2">+1 (917) 6094-597</p>
          <p class="text-sm">
            <a href="mailto:info@zemy-group.com" class="hover:text-gray-400">info@zemy-group.com</a>
          </p>
        </div>
    
        <!-- Existing section: Social Media Icons -->
        <div class="flex justify-center md:justify-end space-x-4">
          <a href="#" class="text-white hover:text-gray-400"><i class="fab fa-facebook-f"></i></a>
          <a href="#" class="text-white hover:text-gray-400"><i class="fab fa-twitter"></i></a>
          <a href="#" class="text-white hover:text-gray-400"><i class="fab fa-linkedin-in"></i></a>
          <a href="#" class="text-white hover:text-gray-400"><i class="fab fa-instagram"></i></a>
        </div>
      </div>
    </footer>
    
  </div>
</template>

<script setup>
const isMenuOpen = ref(false);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};
const modalVisible = ref(false);
const selectedService = ref(null);
const openModal = (service) => {
  selectedService.value = service;
  modalVisible.value = true;
};

const closeModal = () => {
  modalVisible.value = false;
};
const services = [
  { 
    title: 'Healthcare Consultancy', 
    description: 'A professional service that provides expert advice and guidance to healthcare organizations and professionals. The goal is to improve the efficiency, effectiveness, and overall quality of healthcare delivery.', 
    image: 'https://images.pexels.com/photos/305565/pexels-photo-305565.jpeg' // Update with the correct path to your image
  },
  { 
    title: 'Supply and Management,', 
    description: `Finding, procuring, and managing resources & suppliers for laboratory equipment critical to an organization's operations.`, 
    image: 'https://images.pexels.com/photos/1427107/pexels-photo-1427107.jpeg' // Update with the correct path to your image
  },
  { 
    title: 'Innovation', 
    description: 'We innovate equipment and processes to ensure that your business has the best equipment for the job', 
    image: 'https://images.pexels.com/photos/3861457/pexels-photo-3861457.jpeg' // Update with the correct path to your image
  },
  // Add more services as needed
];
const testimonials = [
  {
    name: 'Jane Doe',
    role: 'CEO, Company Inc.',
    quote: 'This service was amazing! It changed the way we do business and helped us achieve our goals efficiently.',
    image: 'https://images.pexels.com/photos/1181406/pexels-photo-1181406.jpeg' // Update with the correct path to your image
  },
  {
    name: 'John Smith',
    role: 'Product Manager, Tech Co.',
    quote: 'Exceptional quality and outstanding support. Highly recommended for any business looking to improve their workflow.',
    image: 'https://images.pexels.com/photos/3790639/pexels-photo-3790639.jpeg' // Update with the correct path to your image
  },
  {
    name: 'Emily Johnson',
    role: 'Marketing Director, Media Ltd.',
    quote: 'A fantastic experience from start to finish. The team was professional, and the results exceeded our expectations.',
    image: 'https://images.pexels.com/photos/3471390/pexels-photo-3471390.jpeg' // Update with the correct path to your image
  },
  // Add more testimonials as needed
];
const form = ref({
  name: '',
  email: '',
  message: '',
});

const successMessage = ref('');
const errorMessage = ref('');

const handleSubmit = async () => {
  try {
    // Here you would typically send the form data to your server
    // Example using fetch:
    const response = await fetch('/api/contact', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(form.value),
    });

    if (!response.ok) {
      throw new Error('Something went wrong');
    }

    form.value = { name: '', email: '', message: '' }; // Clear form
    successMessage.value = 'Thank you for your message!';
    errorMessage.value = '';
  } catch (error) {
    successMessage.value = '';
    errorMessage.value = 'There was a problem sending your message. Please try again.';
  }
};
</script>
<style>
.mybg{
background-color: rgb(247,247,247);
line-height: 2.25rem;
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
.mydiv{
  background-color: rgb(193,209,220)
}
.mycol{
  background-color: rgb(158,40,41);
}
</style>