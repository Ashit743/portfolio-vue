<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'
import { 
  SunIcon, 
  MoonIcon, 
  BriefcaseIcon, 
  GraduationCapIcon, 
  AwardIcon, 
  ArrowUpIcon 
} from 'lucide-vue-next'
import {
  Card,
  CardContent,
  CardHeader,
  CardTitle,
} from "@/components/ui/card"
import {
  Button
} from "@/components/ui/button"

const isDarkMode = ref(false)
const isLoading = ref(true)
const showScrollTop = ref(false)

const skills = [
  { name: 'Vue.js', level: 90, color: 'hsl(var(--primary))' },
  { name: 'TypeScript/JavaScript', level: 85, color: 'hsl(var(--primary))' },
  { name: 'Tailwind CSS', level: 80, color: 'hsl(var(--primary))' },
  { name: 'Node.js', level: 75, color: 'hsl(var(--primary))' },
  { name: 'C++', level: 75, color: 'hsl(var(--primary))' },
]

const projects = [
  { 
    name: 'Rakshak', 
    description: 'React-based system for improving patient follow-up and care continuity',
    tech: ['React', 'Node.js', 'MongoDB'],
  },
  { 
    name: 'Scientific Tray Component', 
    description: 'Stencil.js web component for scientific trays',
    tech: ['Stencil.js', 'TypeScript', 'Jest'],
  },
  { 
    name: 'E-commerce Book Application', 
    description: 'Full-stack Angular and Flask e-commerce platform',
    tech: ['Angular', 'Flask', 'PostgreSQL'],
  },
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

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const handleScroll = () => {
  showScrollTop.value = window.scrollY > 500
}

const typewriterText = computed(() => [
  "I build web applications.",
  "I solve complex problems.",
  "I create user-friendly interfaces.",
  "I optimize performance.",
  "I love coding."
])

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  
  setTimeout(() => {
    isLoading.value = false
    document.body.style.overflow = 'visible'
  }, 2000)

  // Typewriter effect
  let currentText = 0
  let charIndex = 0
  const typeWriter = () => {
    const txt = typewriterText.value
    if (charIndex < txt[currentText].length) {
      const typewriterEl = document.querySelector(".typewriter")
      if (typewriterEl) {
        typewriterEl.innerHTML += txt[currentText].charAt(charIndex)
        charIndex++
        setTimeout(typeWriter, 100)
      }
    } else {
      setTimeout(() => {
        const typewriterEl = document.querySelector(".typewriter")
        if (typewriterEl) {
          typewriterEl.innerHTML = ""
          currentText = (currentText + 1) % txt.length
          charIndex = 0
          typeWriter()
        }
      }, 2000)
    }
  }
  typeWriter()
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <div :class="{ 'dark': isDarkMode }" class="min-h-screen bg-background text-foreground">
    <!-- Loading Screen -->
    <div v-if="isLoading" class="fixed inset-0 z-50 flex items-center justify-center bg-background">
      <div class="relative">
        <div class="w-16 h-16 border-4 border-primary border-t-transparent rounded-full animate-spin"></div>
        <div class="absolute inset-0 flex items-center justify-center">
          <span class="text-primary text-xl">A</span>
        </div>
      </div>
    </div>

    <!-- Navigation Bar -->
    <nav class="bg-background/80 backdrop-blur-xl p-4 fixed w-full z-10 border-b border-border">
      <div class="container mx-auto flex justify-between items-center">
        <a href="#" class="text-2xl font-bold text-primary">AD</a>
        <div class="space-x-4">
          <Button variant="ghost" asChild>
            <a href="#about">About</a>
          </Button>
          <Button variant="ghost" asChild>
            <a href="#skills">Skills</a>
          </Button>
          <Button variant="ghost" asChild>
            <a href="#experience">Experience</a>
          </Button>
          <Button variant="ghost" asChild>
            <a href="#projects">Projects</a>
          </Button>
        </div>
      </div>
    </nav>

    <Button 
      @click="toggleDarkMode" 
      variant="outline"
      class="fixed top-20 right-4 p-2 z-10"
    >
      <SunIcon v-if="isDarkMode" class="w-6 h-6" />
      <MoonIcon v-else class="w-6 h-6" />
    </Button>
    
    <main class="pt-16">
      <!-- Hero Section -->
      <section class="relative min-h-screen flex items-center justify-center overflow-hidden">
        <div class="hero-bg-shapes absolute inset-0 z-0">
          <div class="absolute top-1/4 left-1/4 w-64 h-64 bg-primary/10 rounded-full filter blur-3xl animate-pulse"></div>
          <div class="absolute bottom-1/4 right-1/4 w-64 h-64 bg-primary/10 rounded-full filter blur-3xl animate-pulse delay-1000"></div>
        </div>
        
        <div class="text-center px-4">
          <h1 class="hero-title text-7xl font-bold mb-4 text-primary">
            Ashit Darurmath
          </h1>
          <p class="hero-subtitle text-3xl text-muted-foreground">Senior Software Engineer</p>
          <div class="mt-8 h-8">
            <span class="typewriter text-xl text-muted-foreground"></span>
          </div>
        </div>
      </section>

      <div class="container mx-auto px-4 py-16">
        <!-- About Section -->
        <section id="about" class="mb-16">
          <Card>
            <CardHeader>
              <CardTitle class="text-3xl font-bold text-center">About Me</CardTitle>
            </CardHeader>
            <CardContent>
              <p class="text-muted-foreground text-center max-w-2xl mx-auto">
                I'm a passionate Senior Software Engineer with expertise in Vue.js, React, and modern web technologies. 
                I love creating responsive and user-friendly web applications that push the boundaries of what's possible on the web.
                With a strong background in both front-end and back-end development, I strive to deliver high-quality, efficient solutions.
              </p>
            </CardContent>
          </Card>
        </section>

        <!-- Skills Section -->
        <section id="skills" class="mb-32">
          <h2 class="text-4xl font-bold mb-16 text-center text-primary">Skills</h2>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-8">
            <Card v-for="skill in skills" :key="skill.name" class="group perspective">
              <CardContent class="p-6">
                <h3 class="text-xl font-semibold mb-4">{{ skill.name }}</h3>
                <div class="w-full bg-muted rounded-full h-3">
                  <div class="h-3 rounded-full transition-all duration-300 bg-primary"
                       :style="{ width: `${skill.level}%` }"></div>
                </div>
              </CardContent>
            </Card>
          </div>
        </section>

        <!-- Experience Section -->
        <section id="experience" class="mb-16">
          <h2 class="text-3xl font-bold mb-8 text-center text-primary">Experience</h2>
          <div class="space-y-8">
            <Card v-for="(exp, index) in experiences" :key="index">
              <CardContent class="p-6">
                <div class="flex items-center mb-4">
                  <BriefcaseIcon class="w-6 h-6 mr-2 text-primary" />
                  <h3 class="text-xl font-semibold">{{ exp.role }} at {{ exp.company }}</h3>
                </div>
                <p class="text-muted-foreground mb-4">{{ exp.duration }}</p>
                <ul class="list-disc list-inside text-muted-foreground">
                  <li v-for="highlight in exp.highlights" :key="highlight">{{ highlight }}</li>
                </ul>
              </CardContent>
            </Card>
          </div>
        </section>

        <!-- Projects Section -->
        <section id="projects" class="py-20">
          <h2 class="text-4xl font-bold text-center mb-16 text-primary">Featured Projects</h2>
          <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
            <Card v-for="project in projects" 
                  :key="project.name"
                  class="transform hover:scale-105 transition-all duration-300">
              <CardContent class="p-6">
                <h3 class="text-2xl font-bold mb-4">{{ project.name }}</h3>
                <p class="text-muted-foreground mb-4">{{ project.description }}</p>
                <div class="flex flex-wrap gap-2">
                  <span v-for="tech in project.tech" 
                        :key="tech"
                        class="px-3 py-1 rounded-full text-sm bg-primary/20 text-primary">
                    {{ tech }}
                  </span>
                </div>
              </CardContent>
            </Card>
          </div>
        </section>

        <!-- Education Section -->
        <section class="mt-16">
          <Card>
            <CardHeader>
              <CardTitle class="text-3xl font-bold text-center">Education & Certifications</CardTitle>
            </CardHeader>
            <CardContent>
              <div class="flex items-center mb-4">
                <GraduationCapIcon class="w-6 h-6 mr-2 text-primary" />
                <h3 class="text-xl font-semibold">Bachelor's in Electronics and Communication Engineering</h3>
              </div>
              <p class="text-muted-foreground mb-2">KLS Gogte Institute of Technology, Belagavi, India</p>
              <p class="text-muted-foreground">CGPA - 8.76</p>
              
              <div class="mt-6 space-y-4">
                <div class="flex items-center">
                  <AwardIcon class="w-6 h-6 mr-2 text-primary" />
                  <p class="text-muted-foreground">Microsoft Certified: Azure Fundamentals</p>
                </div>
                <div class="flex items-center">
                  <AwardIcon class="w-6 h-6 mr-2 text-primary" />
                  <p class="text-muted-foreground">Stanford: Code in Place</p>
                </div>
              </div>
            </CardContent>
          </Card>
        </section>
      </div>
    </main>

    <!-- Footer -->
    <footer class="bg-background/80 backdrop-blur-xl p-8 mt-16 border-t border-border">
      <div class="container mx-auto text-center">
        <p class="text-muted-foreground">&copy; 2024 Ashit Darurmath. All rights reserved. 
          <span class="inline-block animate-pulse text-destructive">&hearts;</span>
        </p>
      </div>
    </footer>

    <!-- Scroll to Top Button -->
    <Button
      @click="scrollToTop" 
      variant="default"
      class="fixed bottom-4 right-4 p-2 transition-opacity duration-300"
      :class="{ 'opacity-0': !showScrollTop, 'opacity-100': showScrollTop }"
    >
      <ArrowUpIcon class="w-6 h-6" />
    </Button>
  </div>
</template>

<style>
.perspective {
  perspective: 1000px;
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