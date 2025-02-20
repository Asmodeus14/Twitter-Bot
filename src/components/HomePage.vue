<template>
    <div class="min-h-screen flex flex-col items-center justify-center bg-gradient-to-br from-gray-900 via-blue-900 to-gray-900 text-white">
      <!-- Guardian Symbol -->
      <div class="mb-6">
        <GuardianSymbol class="h-24 w-24 text-blue-400" />
      </div>
      
      <!-- Input Field -->
      <div class="w-full max-w-md bg-white/10 p-6 rounded-xl backdrop-blur-md shadow-lg">
        <h1 class="text-2xl font-bold text-center mb-4">Enter URL</h1>
        <input 
          v-model="inputUrl" 
          type="text" 
          placeholder="Paste your URL here..." 
          class="w-full p-3 rounded-lg bg-gray-800 text-white border border-gray-600 focus:border-blue-400 focus:ring-2 focus:ring-blue-400 outline-none transition"
        />
        <button 
          @click="storeUrl" 
          class="w-full mt-4 p-3 bg-blue-500 hover:bg-blue-600 text-white rounded-lg transition"
        >
          Submit
        </button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import GuardianSymbol from './GuardianSymbol.vue';
  
  const inputUrl = ref('');
  
  const storeUrl = () => {
    console.log('Stored URL:', inputUrl.value);
    alert(`URL Stored: ${inputUrl.value}`);
  };
  </script>
  
  <style scoped>
  /* Custom Animations */
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(-10px); }
    to { opacity: 1; transform: translateY(0); }
  }
  
  .fade-in {
    animation: fadeIn 0.5s ease-out;
  }
  </style>
  