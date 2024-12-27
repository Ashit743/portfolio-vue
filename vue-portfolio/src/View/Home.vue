<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'
import { 
  SunIcon, 
  MoonIcon, 
  BriefcaseIcon, 
  GraduationCapIcon, 
  AwardIcon, 
  ArrowUpIcon,
  LinkIcon,
  GithubIcon,
  LinkedinIcon,
  MailIcon
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
  { name: 'Vue.js', level: 90, color: 'bg-green-500' },
  { name: 'TypeScript/JavaScript', level: 85, color: 'bg-blue-500' },
  { name: 'Tailwind CSS', level: 80, color: 'bg-teal-500' },
  { name: 'Node.js', level: 75, color: 'bg-yellow-500' },
  { name: 'C++', level: 75, color: 'bg-purple-500' },
]

const projects = [
  { 
    name: 'Rakshak', 
    description: 'React-based system for improving patient follow-up and care continuity',
    tech: ['React', 'Node.js', 'MongoDB'],
    link: 'https://github.com/yourusername/rakshak'
  },
  { 
    name: 'Scientific Tray Component', 
    description: 'Stencil.js web component for scientific trays',
    tech: ['Stencil.js', 'TypeScript', 'Jest'],
    link: 'https://github.com/yourusername/scientific-tray'
  },
  { 
    name: 'E-commerce Book Application', 
    description: 'Full-stack Angular and Flask e-commerce platform',
    tech: ['Angular', 'Flask', 'PostgreSQL'],
    link: 'https://github.com/yourusername/book-ecommerce'
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

const certifications = [
  { name: 'Microsoft Certified: Azure Fundamentals', issuer: 'Microsoft', date: 'May 2023' },
  { name: 'Stanford: Code in Place', issuer: 'Stanford University', date: 'August 2022' },
]

const toggleDarkMode = () => {
  isDarkMode.value = !isDarkMode.value
  localStorage.setItem('theme', isDarkMode.value ? 'dark' : 'light')
  applyTheme()
}

const applyTheme = () => {
  if (isDarkMode.value) {
    document.documentElement.classList.add('dark')
  } else {
    document.documentElement.classList.remove('dark')
  }
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

  // Check system preference
  const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches
  const savedTheme = localStorage.getItem('theme')
  isDarkMode.value = savedTheme === 'dark' || (savedTheme === null && prefersDark)
  applyTheme()

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
  <div :class="{ 'dark': isDarkMode }" class="min-h-screen bg-background text-foreground transition-colors duration-300">
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
          <Button variant="ghost" asChild>
            <a href="#certifications">Certifications</a>
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
        
        <div class="text-center px-4 z-10">
          <h1 class="hero-title text-7xl font-bold mb-4 text-primary animate-fadeIn">
            Ashit Darurmath
          </h1>
          <p class="hero-subtitle text-3xl text-muted-foreground animate-fadeIn animation-delay-200">Senior Software Engineer</p>
          <div class="mt-8 h-8">
            <span class="typewriter text-xl text-muted-foreground"></span>
          </div>
          <div class="mt-8 flex justify-center space-x-4 animate-fadeIn animation-delay-400">
            <a href="https://github.com/yourusername" target="_blank" rel="noopener noreferrer" class="text-muted-foreground hover:text-primary transition-colors">
              <GithubIcon class="w-6 h-6" />
            </a>
            <a href="https://linkedin.com/in/yourusername" target="_blank" rel="noopener noreferrer" class="text-muted-foreground hover:text-primary transition-colors">
              <LinkedinIcon class="w-6 h-6" />
            </a>
            <a href="mailto:your.email@example.com" class="text-muted-foreground hover:text-primary transition-colors">
              <MailIcon class="w-6 h-6" />
            </a>
          </div>
        </div>
      </section>

      <div class="container mx-auto px-4 py-16">
        <!-- About Section -->
        <section id="about" class="mb-16 scroll-mt-16">
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
        <section id="skills" class="mb-32 scroll-mt-16">
          <h2 class="text-4xl font-bold mb-16 text-center text-primary">Skills</h2>
          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
            <div v-for="skill in skills" :key="skill.name" class="group">
              <Card class="h-full transform transition-all duration-300 hover:scale-105 hover:shadow-lg">
                <CardContent class="p-6 flex flex-col items-center justify-center h-full">
                  <h3 class="text-xl font-semibold mb-4">{{ skill.name }}</h3>
                  <div class="w-24 h-24 relative mb-4">
                    <svg class="w-full h-full transform -rotate-90">
                      <circle
                        cx="48"
                        cy="48"
                        r="44"
                        stroke-width="8"
                        fill="transparent"
                        class="text-muted stroke-current"
                      />
                      <circle
                        cx="48"
                        cy="48"
                        r="44"
                        stroke-width="8"
                        fill="transparent"
                        :class="skill.color"
                        :stroke-dasharray="`${skill.level * 2.76}, 276`"
                        class="stroke-current transform origin-center transition-all duration-500 ease-out group-hover:stroke-dasharray-276"
                      />
                    </svg>
                    <div class="absolute top-0 left-0 w-full h-full flex items-center justify-center">
                      <span class="text-lg font-bold">{{ skill.level }}%</span>
                    </div>
                  </div>
                </CardContent>
              </Card>
            </div>
          </div>
        </section>

        <!-- Experience Section -->
        <section id="experience" class="mb-16 scroll-mt-16">
          <h2 class="text-3xl font-bold mb-8 text-center text-primary">Experience</h2>
          <div class="space-y-8">
            <Card v-for="(exp, index) in experiences" :key="index"
                  class="transform transition-all duration-300 hover:scale-105 hover:shadow-lg">
              <CardContent class="p-6">
                <div class="flex items-center mb-4">
                  <BriefcaseIcon class="w-6 h-6 mr-2 text-primary" />
                  <h3 class="text-xl font-semibold">{{ exp.role }} at {{ exp.company }}</h3>
                </div>
                <p class="text-muted-foreground mb-4">{{ exp.duration }}</p>
                <ul class="list-disc list-inside text-muted-foreground">
                  <li v-for="(highlight, hIndex) in exp.highlights" :key="hIndex" 
                      class="opacity-0 transform translate-y-4"
                      :class="{'animate-fadeIn': !isLoading}"
                      :style="{ animationDelay: `${hIndex * 100 + 200}ms` }">
                    {{ highlight }}
                  </li>
                </ul>
              </CardContent>
            </Card>
          </div>
        </section>

        <!-- Projects Section -->
        <section id="projects" class="py-20 scroll-mt-16">
          <h2 class="text-4xl font-bold text-center mb-16 text-primary">Featured Projects</h2>
          <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
            <Card v-for="project in projects" 
                  :key="project.name"
                  class="transform hover:scale-105 transition-all duration-300 hover:shadow-lg">
              <CardContent class="p-6 flex flex-col h-full">
                <h3 class="text-2xl font-bold mb-4">{{ project.name }}</h3>
                <p class="text-muted-foreground mb-4 flex-grow">{{ project.description }}</p>
                <div class="flex flex-wrap gap-2 mb-4">
                  <span v-for="tech in project.tech" 
                        :key="tech"
                        class="px-3 py-1 rounded-full text-sm bg-primary/20 text-primary">
                    {{ tech }}
                  </span>
                </div>
                <a :href="project.link" target="_blank" rel="noopener noreferrer"
                   class="inline-flex items-center text-primary hover:underline mt-auto">
                  View Project <LinkIcon class="w-4 h-4 ml-2" />
                </a>
              </CardContent>
            </Card>
          </div>
        </section>

        <!-- Certifications Section -->
        <section id="certifications" class="mt-16 scroll-mt-16">
          <h2 class="text-3xl font-bold mb-8 text-center text-primary">Certifications</h2>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
            <Card v-for="cert in certifications" :key="cert.name"
                  class="transform hover:scale-105 transition-all duration-300 hover:shadow-lg">
              <CardContent class="p-6">
                <div class="flex items-center mb-4">
                  <AwardIcon class="w-6 h-6 mr-2 text-primary" />
                  <h3 class="text-xl font-semibold">{{ cert.name }}</h3>
                </div>
                <p class="text-muted-foreground">Issued by: {{ cert.issuer }}</p>
                <p class="text-muted-foreground mt-2">Date: {{ cert.date }}</p>
              </CardContent>
            </Card>
          </div>
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

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-fadeIn {
  animation: fadeIn 0.5s ease-out forwards;
}

.animation-delay-200 {
  animation-delay: 200ms;
}

.animation-delay-400 {
  animation-delay: 400ms;
}

.scroll-mt-16 {
  scroll-margin-top: 4rem;
}
</style>