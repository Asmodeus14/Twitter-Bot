<template>
    <div class="min-h-screen bg-gradient-to-br from-gray-900 via-blue-900 to-gray-900">
        <div class="container mx-auto px-4 py-12">
            <div class="max-w-2xl mx-auto">
                <!-- Header with Guardian Symbol -->
                <div class="text-center mb-12">
                    <GuardianSymbol class="h-20 w-20 mx-auto text-blue-400 mb-4" />
                    <h1 class="text-4xl font-bold text-white mb-2">Tweet Guardian</h1>
                    <p class="text-gray-300 text-lg">Secure your social experience</p>
                </div>

                <!-- Drag & Drop Zone -->
                <div @dragover.prevent="onDragOver" @drop.prevent="onDrop" @dragleave="isDragging = false" :class="['border-4 border-dashed rounded-xl p-8 text-center transition-colors',
                    isDragging ? 'border-blue-400 bg-blue-900/20' : 'border-gray-600 hover:border-blue-500']">
                    <div class="space-y-4">
                        <UploadIcon class="h-12 w-12 mx-auto text-gray-400" />
                        <p class="text-gray-300 text-lg">
                            <span class="text-blue-400 font-medium">Drag and drop</span> your URL file here
                        </p>
                        <p class="text-gray-400">or click to browse</p>
                    </div>
                </div>

                <!-- Uploaded Links -->
                <div v-if="uploadedLinks.length" class="mt-8 space-y-4">
                    <div v-for="(link, index) in uploadedLinks" :key="index"
                        class="bg-white/10 p-4 rounded-lg backdrop-blur-sm transition hover:bg-white/20">
                        <div class="flex items-center justify-between">
                            <span class="text-gray-200 truncate">{{ link }}</span>
                            <button @click="analyzeLink(link)"
                                class="ml-4 px-4 py-2 bg-blue-500 hover:bg-blue-600 text-white rounded-lg transition">
                                Analyze
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { UploadIcon } from '@heroicons/vue/outline';
import GuardianSymbol from './components/GuardianSymbol.vue';

const isDragging = ref(false);
const uploadedLinks = ref([]);

const onDragOver = () => {
    isDragging.value = true;
};

const onDrop = (e) => {
    isDragging.value = false;
    const file = e.dataTransfer.files[0];
    if (file && file.name.endsWith('.url')) {
        readFile(file);
    } else {
        alert('Please drop a valid .url file');
    }
};

const readFile = (file) => {
    const reader = new FileReader();
    reader.onload = (e) => {
        const content = e.target.result;
        const urlMatch = content.match(/URL=(.*)/);
        if (urlMatch && urlMatch[1]) {
            uploadedLinks.value.push(urlMatch[1]);
        }
    };
    reader.readAsText(file);
};

const analyzeLink = (url) => {
    // Add your analysis logic here
    console.log('Analyzing URL:', url);
    alert(`Safety analysis initiated for: ${url}`);
};
</script>

<style>
/* Add custom animations */
@keyframes pulse {
    50% {
        opacity: 0.5;
    }
}

.animate-pulse {
    animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}
</style>