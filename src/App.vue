<script setup lang="ts">
import { ref } from 'vue';

// --- Types ---
interface Project {
  id: number;
  title: string;
  description: string;
  technologies: string[];
  link?: string;
}

interface Achievement {
  id: number;
  title: string;
  date: string;
  description: string;
  image?: string;
}

// --- Data ---
const name = ref("Jhon Mark T. Bago");
const title = ref("Driven Computer Engineering student");

const aboutText = ref(
  "Driven Computer Engineering student seeking opportunities to apply programming, analytical, and technical problem-solving skills in real-world digital environments. Experienced in software development fundamentals, data science concepts, and collaborative leadership, with a strong commitment to continuous learning and innovation in emerging technologies."
);

const achievements = ref<Achievement[]>([
  {
    id: 1,
    title: "2026 ITE Regional Convention Champion in Technology Quiz Bee",
    date: "2026",
    description: "Secured 1st place in the regional Technology Quiz Bee, demonstrating comprehensive knowledge in IT and computer engineering concepts.",
    image: "ITE.jpeg" 
  },
  {
    id: 2,
    title: "16th ICT Roadshow 3rd Place in Quiz Bowl Competition",
    date: "2024", 
    description: "Awarded 3rd place in the competitive ICT Quiz Bowl against multiple regional institutions.",
    image: "ICT.jpg" 
  },
  {
    id: 3,
    title: "DOST Scholar",
    date: "2023 - Present",
    description: "Awarded the prestigious Department of Science and Technology (DOST) undergraduate scholarship based on academic excellence and merit."
  },
  {
    id: 4,
    title: "Civil Service Eligible",
    date: "August 2023",
    description: "Successfully passed the Philippine Civil Service Examination, granting professional civil service eligibility."
  }
]);

const recentProjects = ref<Project[]>([
  {
    id: 1,
    title: "Veterinary Web for Appointments",
    description: "A comprehensive web-based scheduling and appointment management system designed to streamline operations for veterinary clinics.",
    technologies: ["HTML", "CSS", "JavaScript"], 
  },
  {
    id: 2,
    title: "Training Board",
    description: "An interactive training board application for managing educational modules, hardware simulations, and tracking progress.",
    technologies: ["Embedded Design", "Hardware"], 
  }
]);

const skills = ref<string[]>([
  "Vue.js", "Tailwind CSS", "TypeScript", "Python", "Django REST Framework", 
  "C++", "MATLAB", "Hardware Architecture", "Git"
]);

// --- Item Details Modal Logic ---
const selectedItem = ref<Project | Achievement | null>(null);

const openModal = (item: Project | Achievement) => {
  selectedItem.value = item;
  document.body.style.overflow = 'hidden';
};

const closeModal = () => {
  selectedItem.value = null;
  document.body.style.overflow = '';
};

// --- Contact Modal Logic ---
const showContactModal = ref(false);

const openContactModal = () => {
  showContactModal.value = true;
  document.body.style.overflow = 'hidden';
};

const closeContactModal = () => {
  showContactModal.value = false;
  if (!selectedItem.value && !showCvModal.value) {
    document.body.style.overflow = '';
  }
};

// --- CV Modal Logic ---
const showCvModal = ref(false);

const openCvModal = () => {
  showCvModal.value = true;
  document.body.style.overflow = 'hidden';
};

const closeCvModal = () => {
  showCvModal.value = false;
  if (!selectedItem.value && !showContactModal.value) {
    document.body.style.overflow = '';
  }
};
</script>

<template>
  <div class="min-h-screen bg-[#08070d] text-gray-300 font-sans relative overflow-x-hidden">
    
    <!-- Atmospheric Background Glow Blur -->
    <div class="absolute top-[20%] right-[-10%] w-[500px] h-[500px] bg-indigo-900/10 rounded-full blur-[120px] pointer-events-none"></div>
    <div class="absolute top-[40%] left-[-10%] w-[600px] h-[600px] bg-purple-950/10 rounded-full blur-[150px] pointer-events-none"></div>

    <!-- Navigation -->
    <nav class="fixed w-full bg-[#08070d]/80 backdrop-blur-md border-b border-white/5 z-40">
      <div class="max-w-6xl mx-auto px-6 py-4 flex justify-between items-center">
        <div class="font-semibold text-lg tracking-tight text-white hover:opacity-80 transition cursor-pointer">
          Bago
        </div>
        <ul class="flex space-x-6 text-xs tracking-wider uppercase font-medium text-gray-400">
          <li><a href="#about" class="hover:text-white transition duration-200">about</a></li>
          <li><a href="#achievements" class="hover:text-white transition duration-200">achievements</a></li>
          <li><a href="#projects" class="hover:text-white transition duration-200">projects</a></li>
          <li><a href="#skills" class="hover:text-white transition duration-200">skills</a></li>
        </ul>
      </div>
    </nav>

    <!-- Main Content Container -->
    <main class="max-w-6xl mx-auto px-6 pt-12">
      
      <!-- Header / Hero Section -->
      <section class="min-h-screen flex flex-col md:flex-row items-center justify-center gap-12 pt-24 md:pt-0 relative">
        <div class="w-full md:w-1/2 text-left flex flex-col justify-center">
          <div class="flex flex-wrap gap-2 mb-6">
            <span class="px-3 py-1 rounded-full text-[10px] font-medium tracking-wide bg-white/5 border border-white/10 text-gray-400">vue.js</span>
            <span class="px-3 py-1 rounded-full text-[10px] font-medium tracking-wide bg-white/5 border border-white/10 text-gray-400">tailwindcss</span>
            <span class="px-3 py-1 rounded-full text-[10px] font-medium tracking-wide bg-white/5 border border-white/10 text-gray-400">typescript</span>
          </div>
          <h1 class="text-5xl md:text-6xl font-bold tracking-tight text-white mb-1 leading-tight">Hello, I'm</h1>
          <h1 class="text-5xl md:text-6xl font-bold tracking-tight text-transparent bg-clip-text bg-gradient-to-r from-indigo-400 via-indigo-300 to-indigo-600 mb-6 leading-tight">
            {{ name }}
          </h1>
          <p class="text-sm md:text-base text-gray-400 max-w-md leading-relaxed mb-8">{{ title }}</p>
          <div class="flex flex-wrap items-center gap-4">
            
            <button @click="openContactModal" class="bg-indigo-600 hover:bg-indigo-500 text-white text-xs font-semibold px-5 py-3 rounded-lg shadow-lg hover:shadow-indigo-500/20 transition-all duration-300 flex items-center gap-2">
              Get in touch
              <svg xmlns="http://www.w3.org/2000/svg" class="h-3.5 w-3.5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M9 5l7 7-7 7" />
              </svg>
            </button>

            <!-- New View CV Button -->
            <button @click="openCvModal" class="bg-white/5 hover:bg-white/10 text-white border border-white/10 text-xs font-semibold px-5 py-3 rounded-lg transition duration-300 flex items-center gap-2">
              View CV
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
              </svg>
            </button>

            <a href="#about" class="text-gray-400 hover:text-white text-xs font-semibold px-2 py-3 transition duration-300">
              Learn more &rarr;
            </a>
          </div>
        </div>
        <div class="w-full md:w-1/2 flex justify-center md:justify-end">
          <div class="relative w-full max-w-md md:max-w-lg aspect-[4/3] rounded-[2rem] overflow-hidden group border border-white/5 bg-black/40 shadow-2xl">
            <div class="absolute inset-0 bg-gradient-to-tr from-indigo-500/10 via-purple-500/10 to-transparent opacity-50 group-hover:opacity-100 transition duration-500"></div>
            <img src="/image_2.png" alt="Artistic 3D development workstation illustration" class="w-full h-full object-cover transition duration-700 ease-out transform group-hover:scale-[1.02]"/>
          </div>
        </div>
      </section>

      <!-- About Section -->
      <section id="about" class="py-24 border-t border-white/5">
        <h3 class="text-xs uppercase tracking-widest font-semibold text-indigo-400 mb-2">01. Overview</h3>
        <h2 class="text-3xl font-bold text-white mb-6">About Me</h2>
        <p class="text-sm md:text-base text-gray-400 leading-relaxed max-w-3xl">
          {{ aboutText }}
        </p>
      </section>

      <!-- Achievements Section -->
      <section id="achievements" class="py-24 border-t border-white/5">
        <h3 class="text-xs uppercase tracking-widest font-semibold text-indigo-400 mb-2">02. Milestones</h3>
        <h2 class="text-3xl font-bold text-white mb-10">Achievements</h2>
        <div class="space-y-6">
          <div 
            v-for="achievement in achievements" 
            :key="achievement.id" 
            @click="openModal(achievement)"
            class="cursor-pointer bg-white/[0.02] border border-white/5 hover:border-white/10 p-6 rounded-2xl hover:bg-white/[0.04] transition duration-300 group relative overflow-hidden"
          >
            <div class="flex flex-col md:flex-row md:justify-between md:items-start gap-4 mb-2">
              <h4 class="text-lg font-bold text-white group-hover:text-indigo-400 transition pr-8">{{ achievement.title }}</h4>
              <span class="text-xs font-semibold px-3 py-1 bg-indigo-500/10 text-indigo-300 rounded-md whitespace-nowrap">{{ achievement.date }}</span>
            </div>
            <div class="text-xs text-indigo-500 font-semibold flex items-center opacity-0 group-hover:opacity-100 transition-opacity mt-4">
              View details &rarr;
            </div>
            <div v-if="achievement.image" class="absolute bottom-6 right-6 text-gray-500 opacity-50 group-hover:opacity-100 transition-opacity">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
              </svg>
            </div>
          </div>
        </div>
      </section>

      <!-- Recent Projects Section -->
      <section id="projects" class="py-24 border-t border-white/5">
        <h3 class="text-xs uppercase tracking-widest font-semibold text-indigo-400 mb-2">03. Showcase</h3>
        <h2 class="text-3xl font-bold text-white mb-10">Recent Projects</h2>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <div 
            v-for="project in recentProjects" 
            :key="project.id" 
            @click="openModal(project)"
            class="cursor-pointer group bg-white/[0.02] border border-white/5 hover:border-indigo-500/20 p-6 rounded-2xl hover:bg-white/[0.04] transition-all duration-300 flex flex-col justify-between"
          >
            <div>
              <h4 class="text-lg font-bold text-white group-hover:text-indigo-400 transition mb-3">{{ project.title }}</h4>
              <p class="text-gray-400 mb-6 text-sm leading-relaxed line-clamp-2">{{ project.description }}</p>
            </div>
            <div class="flex justify-between items-end mt-auto">
              <div class="flex flex-wrap gap-2">
                <span v-for="tech in project.technologies.slice(0,3)" :key="tech" class="px-2.5 py-1 bg-white/5 text-gray-300 text-[10px] font-medium rounded-full border border-white/5">
                  {{ tech }}
                </span>
                <span v-if="project.technologies.length > 3" class="px-2.5 py-1 text-gray-500 text-[10px] font-medium">
                  +{{ project.technologies.length - 3 }}
                </span>
              </div>
              <div class="text-xs text-indigo-500 font-semibold opacity-0 group-hover:opacity-100 transition-opacity">
                Explore &rarr;
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Skills Section -->
      <section id="skills" class="py-24 border-t border-white/5">
        <h3 class="text-xs uppercase tracking-widest font-semibold text-indigo-400 mb-2">04. Expertise</h3>
        <h2 class="text-2xl font-bold text-white mb-10">Skills & Technologies</h2>
        <div class="flex flex-wrap gap-3">
          <div 
            v-for="skill in skills" 
            :key="skill" 
            class="px-5 py-2.5 bg-white/[0.02] border border-white/10 rounded-xl text-sm text-gray-300 font-medium hover:border-indigo-500/50 hover:text-indigo-300 hover:bg-indigo-500/10 transition-all duration-300 cursor-default"
          >
            {{ skill }}
          </div>
        </div>
      </section>

    </main>

    <!-- Floating Modal Overlay for CV Preview -->
    <transition name="fade">
      <div 
        v-if="showCvModal" 
        class="fixed inset-0 z-[100] flex items-center justify-center p-4 sm:p-6"
      >
        <div 
          class="absolute inset-0 bg-black/80 backdrop-blur-md cursor-pointer" 
          @click="closeCvModal"
        ></div>

        <div class="relative w-full max-w-4xl h-[85vh] bg-[#0d0c14] border border-white/10 rounded-3xl shadow-2xl p-6 md:p-8 transform transition-all flex flex-col">
          
          <!-- Modal Header & Close Button -->
          <div class="flex justify-between items-center mb-6">
            <h3 class="text-2xl font-bold text-white">Curriculum Vitae</h3>
            <button 
              @click="closeCvModal" 
              class="text-gray-400 hover:text-white bg-white/5 hover:bg-white/20 rounded-full p-2 transition-colors duration-200"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
          </div>
          
          <!-- PDF Preview Iframe -->
          <div class="flex-grow bg-white/5 rounded-xl border border-white/10 overflow-hidden mb-6">
            <iframe src="/resume.pdf" class="w-full h-full" frameborder="0" title="CV Preview"></iframe>
          </div>

          <!-- Download Button -->
          <div class="flex justify-end">
            <!-- Replace href with actual path and name it how you want it to download -->
            <a href="/resume.pdf" download="Bago, Jhon Mark T._Resume.pdf" class="bg-indigo-600 hover:bg-indigo-500 text-white text-sm font-semibold px-6 py-3 rounded-xl shadow-lg hover:shadow-indigo-500/20 transition-all duration-300 flex items-center gap-2">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
              </svg>
              Download CV
            </a>
          </div>

        </div>
      </div>
    </transition>

    <!-- Floating Modal Overlay for Contact -->
    <transition name="fade">
      <div 
        v-if="showContactModal" 
        class="fixed inset-0 z-[100] flex items-center justify-center p-4 sm:p-6"
      >
        <div 
          class="absolute inset-0 bg-black/80 backdrop-blur-md cursor-pointer" 
          @click="closeContactModal"
        ></div>

        <div class="relative w-full max-w-sm bg-[#0d0c14] border border-white/10 rounded-3xl shadow-2xl p-8 transform transition-all text-center">
          
          <button 
            @click="closeContactModal" 
            class="absolute top-6 right-6 text-gray-400 hover:text-white bg-white/5 hover:bg-white/20 rounded-full p-2 transition-colors duration-200"
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>

          <h3 class="text-2xl font-bold text-white mb-6">Let's Connect</h3>
          
          <div class="flex flex-col gap-4 text-left bg-white/[0.03] border border-white/5 p-5 rounded-2xl mb-8">
            <div class="flex items-center gap-3">
              <svg class="w-5 h-5 text-indigo-400 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" /></svg>
              <span class="text-gray-300 text-sm font-medium break-all">jhonmarkbago@gmail.com</span>
            </div>
            <div class="flex items-center gap-3">
              <svg class="w-5 h-5 text-indigo-400 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" /></svg>
              <span class="text-gray-300 text-sm font-medium">+63 928 195 4787</span>
            </div>
            <div class="flex items-center gap-3">
              <svg class="w-5 h-5 text-indigo-400 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.243-4.243a8 8 0 1111.314 0z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" /></svg>
              <span class="text-gray-300 text-sm font-medium">Solana, Cagayan, Philippines</span>
            </div>
          </div>
          
          <div class="flex flex-col gap-4">
            <a href="https://www.linkedin.com/in/jhonmarkbago/" target="_blank" class="flex items-center justify-center gap-3 w-full py-3 px-4 bg-[#0A66C2] hover:bg-[#004182] text-white font-semibold rounded-xl transition duration-300">
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/></svg>
              LinkedIn
            </a>
            <a href="https://www.facebook.com/jhonmark.bago" target="_blank" class="flex items-center justify-center gap-3 w-full py-3 px-4 bg-[#1877F2] hover:bg-[#0C5BCE] text-white font-semibold rounded-xl transition duration-300">
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M9 8h-3v4h3v12h5v-12h3.642l.358-4h-4v-1.667c0-.955.192-1.333 1.115-1.333h2.885v-5h-3.808c-3.596 0-5.192 1.583-5.192 4.615v3.385z"/></svg>
              Facebook
            </a>
          </div>
        </div>
      </div>
    </transition>

    <!-- Floating Modal Overlay for Projects/Achievements Details -->
    <transition name="fade">
      <div 
        v-if="selectedItem" 
        class="fixed inset-0 z-[100] flex items-center justify-center p-4 sm:p-6"
      >
        <div 
          class="absolute inset-0 bg-black/80 backdrop-blur-md cursor-pointer" 
          @click="closeModal"
        ></div>

        <div class="relative w-full max-w-2xl bg-[#0d0c14] border border-white/10 rounded-3xl shadow-2xl p-6 md:p-8 transform transition-all overflow-y-auto max-h-[90vh]">
          
          <button 
            @click="closeModal" 
            class="absolute top-6 right-6 text-gray-400 hover:text-white bg-white/5 hover:bg-white/20 rounded-full p-2 transition-colors duration-200 z-10"
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>

          <div v-if="'image' in selectedItem && selectedItem.image" class="mb-6 rounded-xl overflow-hidden border border-white/10 w-full h-48 md:h-64">
            <img :src="selectedItem.image" alt="Achievement Media" class="w-full h-full object-cover" />
          </div>

          <h3 class="text-2xl md:text-3xl font-bold text-white pr-10 mb-3 mt-2">
            {{ selectedItem.title }}
          </h3>
          
          <div v-if="'date' in selectedItem" class="mb-6">
            <span class="inline-block px-3 py-1 bg-indigo-500/20 border border-indigo-500/30 text-indigo-300 text-xs font-semibold rounded-md">
              {{ selectedItem.date }}
            </span>
          </div>
          
          <div v-else class="h-2"></div>

          <div class="prose prose-invert max-w-none">
            <p class="text-gray-300 text-base leading-relaxed mb-8">
              {{ selectedItem.description }}
            </p>
          </div>

          <div v-if="'technologies' in selectedItem" class="flex flex-wrap gap-2 mt-auto pt-6 border-t border-white/5">
            <span 
              v-for="tech in selectedItem.technologies" 
              :key="tech" 
              class="px-3 py-1.5 bg-indigo-500/10 text-indigo-300 text-xs font-semibold rounded-md border border-indigo-500/20"
            >
              {{ tech }}
            </span>
          </div>
        </div>
      </div>
    </transition>
    
    <!-- Footer -->
    <footer class="border-t border-white/5 bg-black/40 py-8 text-center mt-24">
      <p class="text-gray-500 text-xs tracking-wider">© 2026 {{ name }} Built with Vue 3 & Tailwind CSS v4.</p>
    </footer>
  </div>
</template>

<style>
/* Smooth fade animation for the modals */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>