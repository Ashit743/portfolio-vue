<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'
import { SunIcon, MoonIcon, ChevronLeftIcon, ChevronRightIcon, BriefcaseIcon, GraduationCapIcon, AwardIcon, ArrowUpIcon } from 'lucide-vue-next'
import { useIntervalFn } from '@vueuse/core'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import { TextPlugin } from 'gsap/TextPlugin'
import ashitAvatar from '@/components/ashitAvatar.vue'
gsap.registerPlugin(ScrollTrigger, TextPlugin)

const isDarkMode = ref(false)
const currentProjectIndex = ref(0)
const isLoading = ref(true)
const showScrollTop = ref(false)

const skills = [
  { name: 'Vue.js', level: 90 },
  { name: 'TypeScript/JavaScript', level: 85 },
  { name: 'Tailwind CSS', level: 80 },
  { name: 'Node.js', level: 75 },
  { name: 'C++', level: 75 },
]

const projects = [
  { name: 'Rakshak', description: 'React-based system for improving patient follow-up and care continuity', image: 'https://via.placeholder.com/600x400.png?text=Rakshak' },
  { name: 'Scientific Tray Component', description: 'Stencil.js web component for scientific trays', image: 'https://via.placeholder.com/600x400.png?text=Scientific+Tray' },
  { name: 'E-commerce Book Application', description: 'Full-stack Angular and Flask e-commerce platform', image: 'https://via.placeholder.com/600x400.png?text=E-commerce+App' },
  { name: 'GMT-based Date Handling System', description: 'Pinia-powered date handling system for Vue.js', image: 'https://via.placeholder.com/600x400.png?text=Date+Handling+System' },
]

const experiences = [
  {
    company: 'Persistent Systems',
    role: 'Senior Software Engineer',
    duration: 'June 2024 - Present',
    highlights: [
      'Reduced application vulnerabilities by 65%',
      'Slashed unit test execution time by 78%',
      'Integrated Storybook into Vue.js application',
    ],
  },
  {
    company: 'Persistent Systems',
    role: 'Software Engineer',
    duration: 'June 2022 - June 2024',
    highlights: [
      'Developed Stencil.js scientific tray web component',
      'Architected OOP-based TypeScript solution for autosampler data',
      'Implemented "Debug Mode" with live editor',
    ],
  },
]

const toggleDarkMode = () => {
  isDarkMode.value = !isDarkMode.value
  document.documentElement.classList.toggle('dark')
}

const nextProject = () => {
  gsap.to('.project-slide', { 
    x: '-100%', 
    opacity: 0, 
    duration: 0.5, 
    onComplete: () => {
      currentProjectIndex.value = (currentProjectIndex.value + 1) % projects.length
      gsap.fromTo('.project-slide', 
        { x: '100%', opacity: 0 }, 
        { x: '0%', opacity: 1, duration: 0.5 }
      )
    }
  })
}

const prevProject = () => {
  gsap.to('.project-slide', { 
    x: '100%', 
    opacity: 0, 
    duration: 0.5, 
    onComplete: () => {
      currentProjectIndex.value = (currentProjectIndex.value - 1 + projects.length) % projects.length
      gsap.fromTo('.project-slide', 
        { x: '-100%', opacity: 0 }, 
        { x: '0%', opacity: 1, duration: 0.5 }
      )
    }
  })
}

const { pause, resume } = useIntervalFn(() => {
  nextProject()
}, 5000)

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const handleScroll = () => {
  showScrollTop.value = window.scrollY > 500
}

onMounted(() => {
  resume()
  animateHero()
  animateSkills()
  animateSections()
  window.addEventListener('scroll', handleScroll)
  
  // Simulate loading
  setTimeout(() => {
    isLoading.value = false
    document.body.style.overflow = 'visible'
  }, 2000)

    // Typewriter effect
    let i = 0;
  const txt = typewriterText.value;
  let charIndex = 0;
  let currentText = 0;
  const typeWriter = () => {
    if (charIndex < txt[currentText].length) {
      document.querySelector(".typewriter").innerHTML += txt[currentText].charAt(charIndex);
      charIndex++;
      setTimeout(typeWriter, 100);
    } else {
      setTimeout(() => {
        document.querySelector(".typewriter").innerHTML = "";
        currentText = (currentText + 1) % txt.length;
        charIndex = 0;
        typeWriter();
      }, 2000);
    }
  }
  typeWriter();
})

onUnmounted(() => {
  pause()
  window.removeEventListener('scroll', handleScroll)
})

const animateHero = () => {
  const tl = gsap.timeline()
  tl.from('.hero-title', { opacity: 0, y: 50, duration: 1, ease: 'power3.out' })
    .from('.hero-subtitle', { opacity: 0, y: 20, duration: 1, ease: 'power3.out' }, '-=0.5')
}

const animateSkills = () => {
  gsap.from('.skill-bar', {
    width: 0,
    duration: 1.5,
    ease: 'power2.out',
    stagger: 0.2,
    scrollTrigger: {
      trigger: '.skills-section',
      start: 'top 80%',
    },
  })
}

const animateSections = () => {
  gsap.utils.toArray('.animate-section').forEach((section, i) => {
    gsap.from(section, {
      opacity: 0,
      y: 50,
      duration: 1,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: section,
        start: 'top 80%',
      },
    })
  })
}

const typewriterText = computed(() => {
  return [
    "I build web applications.",
    "I solve complex problems.",
    "I create user-friendly interfaces.",
    "I optimize performance.",
    "I love coding."
  ]
})
</script>

<template>
  <div :class="{ 'dark': isDarkMode }" class="min-h-screen bg-gradient-to-br from-blue-50 to-purple-50 dark:from-gray-900 dark:to-blue-900 text-gray-900 dark:text-white transition-colors duration-300">
    <!-- Loading Screen -->
    <div v-if="isLoading" class="fixed inset-0 z-50 flex items-center justify-center bg-white dark:bg-gray-900">
      <div class="text-4xl font-bold text-blue-600 dark:text-blue-400">
        <span class="animate-pulse">Loading...</span>
        <span class="animate-bounce">.</span>
        <span class="animate-bounce delay-100">.</span>
        <span class="animate-bounce delay-200">.</span>
      </div>
    </div>

    <!-- Navigation Bar -->
    <nav class="bg-white bg-opacity-80 dark:bg-gray-800 dark:bg-opacity-80 backdrop-filter backdrop-blur-lg p-4 fixed w-full z-10">
      <div class="container mx-auto flex justify-between items-center">
        <a href="#" class="text-2xl font-bold text-blue-600 dark:text-blue-400"><ashitAvatar/></a>
        <div class="space-x-4">
          <a href="#about" class="hover:text-blue-600 dark:hover:text-blue-400 transition-colors duration-300">About</a>
          <a href="#skills" class="hover:text-blue-600 dark:hover:text-blue-400 transition-colors duration-300">Skills</a>
          <a href="#experience" class="hover:text-blue-600 dark:hover:text-blue-400 transition-colors duration-300">Experience</a>
          <a href="#projects" class="hover:text-blue-600 dark:hover:text-blue-400 transition-colors duration-300">Projects</a>
        </div>
      </div>
    </nav>

    <button 
      @click="toggleDarkMode" 
      class="fixed top-20 right-4 p-2 rounded-full bg-white dark:bg-gray-800 text-blue-600 dark:text-blue-400 shadow-lg z-10 transition-colors duration-300"
    >
      <SunIcon v-if="isDarkMode" class="w-6 h-6" />
      <MoonIcon v-else class="w-6 h-6" />
    </button>
    
    <main class="pt-16">
      <!-- Hero Section -->
      <section class="relative h-screen flex items-center justify-center overflow-hidden">
        <div class="text-center">
          <h1 class="hero-title text-6xl font-bold mb-4 text-blue-600 dark:text-blue-400">Ashit Darurmath</h1>
          <p class="hero-subtitle text-2xl text-gray-600 dark:text-gray-300">Senior Software Engineer</p>
          <div class="mt-4 h-8">
            <span class="typewriter text-xl text-gray-600 dark:text-gray-300"></span>
          </div>
        </div>
        <div class="absolute inset-0 z-0">
          <div class="absolute inset-0 bg-gradient-to-r from-blue-500 to-purple-500 opacity-20 dark:opacity-40"></div>
        </div>
      </section>

      <div class="container mx-auto px-4 py-16">
        <section id="about" class="mb-16 animate-section">
          <h2 class="text-3xl font-bold mb-8 text-center text-blue-600 dark:text-blue-400">About Me</h2>
          <p class="text-gray-600 dark:text-gray-300 text-center max-w-2xl mx-auto">
            I'm a passionate Senior Software Engineer with expertise in Vue.js, React, and modern web technologies. 
            I love creating responsive and user-friendly web applications that push the boundaries of what's possible on the web.
            With a strong background in both front-end and back-end development, I strive to deliver high-quality, efficient solutions.
          </p>
        </section>

        <section id="skills" class="mb-16 skills-section animate-section">
          <h2 class="text-3xl font-bold mb-8 text-center text-blue-600 dark:text-blue-400">Skills</h2>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
            <div v-for="skill in skills" :key="skill.name" class="bg-white dark:bg-gray-800 rounded-lg p-4 shadow-lg">
              <h3 class="text-xl font-semibold mb-2">{{ skill.name }}</h3>
              <div class="w-full bg-gray-200 dark:bg-gray-700 rounded-full h-2.5">
                <div class="skill-bar bg-blue-600 dark:bg-blue-400 h-2.5 rounded-full" :style="{ width: `${skill.level}%` }"></div>
              </div>
            </div>
          </div>
        </section>

        <section id="experience" class="mb-16 animate-section">
          <h2 class="text-3xl font-bold mb-8 text-center text-blue-600 dark:text-blue-400">Experience</h2>
          <div class="space-y-8">
            <div v-for="(exp, index) in experiences" :key="index" class="bg-white dark:bg-gray-800 rounded-lg p-6 shadow-lg">
              <div class="flex items-center mb-4">
                <BriefcaseIcon class="w-6 h-6 mr-2 text-blue-600 dark:text-blue-400" />
                <h3 class="text-xl font-semibold">{{ exp.role }} at {{ exp.company }}</h3>
              </div>
              <p class="text-gray-600 dark:text-gray-300 mb-4">{{ exp.duration }}</p>
              <ul class="list-disc list-inside text-gray-600 dark:text-gray-300">
                <li v-for="highlight in exp.highlights" :key="highlight">{{ highlight }}</li>
              </ul>
            </div>
          </div>
        </section>

        <section id="projects" class="animate-section">
          <h2 class="text-3xl font-bold mb-8 text-center text-blue-600 dark:text-blue-400">Projects</h2>
          <div class="relative overflow-hidden">
            <div class="project-slide">
              <div class="bg-white dark:bg-gray-800 rounded-lg overflow-hidden shadow-lg">
                <img 
                  :src="projects[currentProjectIndex].image" 
                  :alt="projects[currentProjectIndex].name" 
                  class="w-full h-64 object-cover"
                />
                <div class="p-6">
                  <h3 class="text-xl font-semibold mb-2">{{ projects[currentProjectIndex].name }}</h3>
                  <p class="text-gray-600 dark:text-gray-300">{{ projects[currentProjectIndex].description }}</p>
                </div>
              </div>
            </div>
            <button @click="prevProject" class="absolute top-1/2 left-4 transform -translate-y-1/2 bg-white dark:bg-gray-800 rounded-full p-2 shadow-lg">
              <ChevronLeftIcon class="w-6 h-6 text-blue-600 dark:text-blue-400" />
            </button>
            <button @click="nextProject" class="absolute top-1/2 right-4 transform -translate-y-1/2 bg-white dark:bg-gray-800 rounded-full p-2 shadow-lg">
              <ChevronRightIcon class="w-6 h-6 text-blue-600 dark:text-blue-400" />
            </button>
          </div>
        </section>

        <section class="mt-16 animate-section">
          <h2 class="text-3xl font-bold mb-8 text-center text-blue-600 dark:text-blue-400">Education & Certifications</h2>
          <div class="bg-white dark:bg-gray-800 rounded-lg p-6 shadow-lg">
            <div class="flex items-center mb-4">
              <GraduationCapIcon class="w-6 h-6 mr-2 text-blue-600 dark:text-blue-400" />
              <h3 class="text-xl font-semibold">Bachelor's in Electronics and Communication Engineering</h3>
            </div>
            <p class="text-gray-600 dark:text-gray-300 mb-2">KLS Gogte Institute of Technology, Belagavi, India</p>
            <p class="text-gray-600 dark:text-gray-300">CGPA - 8.76</p>
          </div>
          <div class="mt-6 space-y-4">
            <div class="flex items-center">
              <AwardIcon class="w-6 h-6 mr-2 text-blue-600 dark:text-blue-400" />
              <p class="text-gray-600 dark:text-gray-300">Microsoft Certified: Azure Fundamentals</p>
            </div>
            <div class="flex items-center">
              <AwardIcon class="w-6 h-6 mr-2 text-blue-600 dark:text-blue-400" />
              <p class="text-gray-600 dark:text-gray-300">Stanford: Code in Place</p>
            </div>
          </div>
        </section>
      </div>
    </main>

    <!-- Footer -->
    <footer class="bg-white bg-opacity-80 dark:bg-gray-800 dark:bg-opacity-80 backdrop-filter backdrop-blur-lg p-4 mt-16">
      <div class="container mx-auto text-center">
        <p class="text-gray-600 dark:text-gray-300">&copy; 2024 Ashit Darurmath. All rights reserved. <span class="text-red-500">&hearts;</span></p>
      </div>
    </footer>

    <!-- Scroll to Top Button -->
    <button 
      @click="scrollToTop" 
      class="fixed bottom-4 right-4 p-2 rounded-full bg-blue-600 text-white shadow-lg transition-opacity duration-300"
      :class="{ 'opacity-0': !showScrollTop, 'opacity-100': showScrollTop }"
    >
      <ArrowUpIcon class="w-6 h-6" />
    </button>
  </div>
</template>

<style>
@import 'tailwindcss/base';
@import 'tailwindcss/components';
@import 'tailwindcss/utilities';

:root {
  --foreground-rgb: 0, 0, 0;
  --background-start-rgb: 214, 219, 220;
  --background-end-rgb: 255, 255, 255;
}

.dark {
  --foreground-rgb: 255, 255, 255;
  --background-start-rgb: 0, 0, 0;
  --background-end-rgb: 0, 0, 0;
}

body {
  color: rgb(var(--foreground-rgb));
  background: linear-gradient(
      to bottom,
      transparent,
      rgb(var(--background-end-rgb))
    )
    rgb(var(--background-start-rgb));
  overflow: hidden;
}

.project-slide {
  transition: transform 0.5s ease-in-out;
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

.animate-float {
  animation: float 3s ease-in-out infinite;
}

.typewriter::after {
  content: '|';
  animation: blink 0.7s infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}
</style>
