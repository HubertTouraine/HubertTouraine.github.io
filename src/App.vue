<script setup>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

const activeProject = ref(0);
const currentImageIndex = ref(0);

// Reset image index when project changes
const setActiveProject = (index) => {
  if (activeProject.value !== index) {
    activeProject.value = index;
    currentImageIndex.value = 0;
  }
};

const nextImage = () => {
  const images = projects.value[activeProject.value].images;
  if (images && images.length > 0) {
    currentImageIndex.value = (currentImageIndex.value + 1) % images.length;
  }
};

const prevImage = () => {
  const images = projects.value[activeProject.value].images;
  if (images && images.length > 0) {
    currentImageIndex.value = (currentImageIndex.value - 1 + images.length) % images.length;
  }
};

const profile = {
  name: 'Hubert Touraine',
  title: 'Epitech Student & Full Stack Developer',
  description: 'Currently a 3rd-year student at Epitech, specializing in Full Stack development with a focus on modern architectures and user experience.',
  email: 'huberttouraine@gmail.com',
  phone: '07 87 30 38 97',
  linkedin: 'https://www.linkedin.com/in/hubert-touraine-899b60228',
};

const experiences = ref([
  {
    role: 'Backend Web Development Intern',
    company: 'Vermeg',
    period: '09/2024 - 12/2024',
    details: [
      'Developed interbank contract automation software.',
      'API integration.',
      'Utilized Python.'
    ]
  }
]);

const education = ref([
  {
    school: 'EPITECH TECHNOLOGY',
    degree: 'Computer Science and Innovation',
    period: '2023 - 2028'
  },
  {
    school: 'ICAM / IUT de Sénart',
    degree: 'Dual degree: General Engineering / Industrial Engineering',
    period: '2022 - 2023'
  },
  {
    school: 'Lycée Claude Bernard',
    degree: 'High School Diploma (Maths / Computer Science)',
    period: '2019 - 2022'
  }
]);

const projects = ref([
  {
    title: 'AREA',
    subtitle: 'Automation Platform (IFTTT-style)',
    description: 'Full-stack development (server, web, mobile) to connect services (Gmail, OneDrive, etc.) via automated actions/reactions.',
    tags: ['Vue.js', 'React Native', 'Go', 'Docker', 'OAuth2'],
    images: [],
    link: '#'
  },
  {
    title: 'ARCADE',
    subtitle: 'C++ Game Engine (OOP)',
    description: 'Creation of a virtual arcade machine with games (Pac-Man, Snake) supporting 3 graphical libraries (SFML, ncurses, SDL2).',
    tags: ['C++', 'OOP', 'SFML', 'SDL2'],
    images: [],
    link: '#'
  },
  {
    title: 'Vueling Hackathon',
    subtitle: 'Finalist - "Smart Voice Recognition"',
    description: "Developed a local AI solution for real-time voice recognition and translation on aircraft. This system facilitates seamless communication between crew and passengers by providing instant transcription and multi-language support without requiring an internet connection.",
    tags: ['AI', 'Python', 'Real-time', 'Innovation'],
    images: ['/projects/vueling1.png', '/projects/vueling2.png'],
    link: '#'
  },
  {
    title: 'Hackathon Onepoint',
    subtitle: 'Eco-Tech Challenge',
    description: 'Chatbot to raise awareness about the environmental impact of LLMs and promote eco-responsible AI.',
    tags: ['LLM', 'Green AI', 'Chatbot'],
    images: [],
    link: '#'
  }
]);

const skills = ref([
  'VS Code', 'GitHub', 'Jira', 'Notion', 'C', 'C++', 'Python', 'Vue.js', 'Docker'
]);

onMounted(() => {
  // Initial Entrance Animation
  const tl = gsap.timeline();

  tl.from('.navbar', {
    y: -50,
    opacity: 0,
    duration: 1,
    ease: 'power3.out'
  })
  .from('.hero-title', {
    y: 50,
    opacity: 0,
    duration: 1,
    ease: 'power3.out'
  }, '-=0.5')
  .from('.hero-desc', {
    y: 30,
    opacity: 0,
    duration: 0.8,
    ease: 'power3.out'
  }, '-=0.6')
  .from('.tech-pill', {
    y: 20,
    opacity: 0,
    duration: 0.5,
    stagger: 0.1,
    ease: 'back.out(1.7)'
  }, '-=0.4');

  // Scroll Animations for Sections
  gsap.utils.toArray('.section-title').forEach(title => {
    gsap.from(title, {
      scrollTrigger: {
        trigger: title,
        start: 'top 80%',
        toggleActions: 'play none none reverse'
      },
      y: 30,
      opacity: 0,
      duration: 0.8,
      ease: 'power3.out'
    });
  });

  gsap.from('.nav-item-wrapper', {
    scrollTrigger: {
      trigger: '#projects',
      start: 'top 90%',
      toggleActions: 'play none none reverse'
    },
    y: 50,
    opacity: 0,
    duration: 0.8,
    stagger: 0.1,
    ease: 'power3.out',
    clearProps: 'all' // Critical: remove inline styles after animation so CSS hover works
  });

  gsap.from('.timeline-item', {
    scrollTrigger: {
      trigger: '.timeline',
      start: 'top 80%'
    },
    x: -30,
    opacity: 0,
    duration: 0.8,
    stagger: 0.2,
    ease: 'power3.out'
  });
  
  gsap.from('.edu-card', {
      scrollTrigger: {
        trigger: '.education-list',
        start: 'top 80%'
      },
      x: 30,
      opacity: 0,
      duration: 0.8,
      stagger: 0.2,
      ease: 'power3.out'
    });

  gsap.from('.footer-card', {
    scrollTrigger: {
      trigger: '.footer',
      start: 'top 90%'
    },
    scale: 0.95,
    opacity: 0,
    duration: 1,
    ease: 'power3.out'
  });

  // Mouse Glow Effect Tracking (Optional for the new layout)
  const windowEl = document.querySelector('.preview-window');
  if (windowEl) {
    windowEl.addEventListener('mousemove', (e) => {
      const rect = windowEl.getBoundingClientRect();
      const x = e.clientX - rect.left;
      const y = e.clientY - rect.top;
      windowEl.style.setProperty('--mouse-x', `${x}px`);
      windowEl.style.setProperty('--mouse-y', `${y}px`);
    });
  }
});
</script>

<template>
  <div class="app-wrapper">
    <!-- Grid Background -->
    <div class="bg-grid"></div>
    <div class="bg-glow"></div>

    <nav class="navbar">
      <div class="container nav-content">
        <a href="#" class="logo">HT<span class="dot">.</span></a>
        <div class="nav-links">
          <a href="#projects">Projects</a>
          <a href="#experience">Experience</a>
          <a href="#contact" class="btn-contact">Contact Me</a>
        </div>
      </div>
    </nav>

    <main class="container main-content">
      <!-- Hero -->
      <header class="hero">
        <h1 class="hero-title">
          Hubert Touraine
          <span class="block-gradient">Full Stack Developer</span>
        </h1>
        <p class="hero-desc">
          Epitech student, I design high-performance and innovative digital solutions. 
          Passionate about software architecture and user experience.
        </p>
        
        <div class="tech-stack-hero">
          <span v-for="skill in skills" :key="skill" class="tech-pill">{{ skill }}</span>
        </div>
      </header>

      <!-- Projects Showcase (Split Layout) -->
      <section id="projects" class="section projects-showcase">
        <div class="showcase-container">
          <!-- Left: Navigable List -->
          <div class="projects-nav">
            <h2 class="showcase-title">Selected <span class="highlight">Works</span></h2>
            <div class="nav-items">
              <div 
                v-for="(project, index) in projects" 
                :key="index"
                class="nav-item-wrapper"
                @mouseenter="setActiveProject(index)"
                :class="{ active: activeProject === index }"
              >
                <div class="nav-item">
                  <span class="nav-index">0{{ index + 1 }}</span>
                  <div class="nav-meta">
                    <h3 class="nav-title">{{ project.title }}</h3>
                    <span class="nav-subtitle">{{ project.subtitle }}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Right: Dynamic Preview Area -->
          <div class="project-preview-stage">
            <div class="preview-window">
              <transition name="preview-fade" mode="out-in">
                <div :key="activeProject" class="preview-content">
                  <div class="preview-media-placeholder">
                    <div class="media-inner">
                      <!-- Project Slider -->
                      <div v-if="projects[activeProject].images && projects[activeProject].images.length" class="slider-container">
                        <transition name="slide-fade" mode="out-in">
                          <img 
                            :key="currentImageIndex" 
                            :src="projects[activeProject].images[currentImageIndex]" 
                            class="preview-img" 
                            alt="Project Preview" 
                          />
                        </transition>

                        <!-- Navigation Arrows -->
                        <div v-if="projects[activeProject].images.length > 1" class="slider-controls">
                          <button @click.stop="prevImage" class="slider-btn prev">
                            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="15 18 9 12 15 6"></polyline></svg>
                          </button>
                          <button @click.stop="nextImage" class="slider-btn next">
                            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="9 18 15 12 9 6"></polyline></svg>
                          </button>
                        </div>

                        <!-- Pagination Dots -->
                        <div v-if="projects[activeProject].images.length > 1" class="slider-dots">
                          <span 
                            v-for="(_, i) in projects[activeProject].images" 
                            :key="i"
                            class="dot-indicator"
                            :class="{ active: currentImageIndex === i }"
                            @click.stop="currentImageIndex = i"
                          ></span>
                        </div>
                      </div>
                      
                      <!-- Stylized placeholder -->
                      <div v-else class="placeholder-icon">
                        <svg width="60" height="60" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="18" height="18" rx="2" ry="2"></rect><circle cx="8.5" cy="8.5" r="1.5"></circle><polyline points="21 15 16 10 5 21"></polyline></svg>
                        <span>Preview Frame</span>
                      </div>
                    </div>
                  </div>
                  <div class="preview-details">
                    <p class="preview-desc">{{ projects[activeProject].description }}</p>
                    <div class="preview-tags">
                      <span v-for="tag in projects[activeProject].tags" :key="tag" class="micro-tag">{{ tag }}</span>
                    </div>
                  </div>
                </div>
              </transition>
            </div>
          </div>
        </div>
      </section>

      <!-- Experience & Education -->
      <section id="experience" class="section split-section">
        <div class="col">
          <h2 class="section-title">Experience</h2>
          <div class="timeline">
            <div v-for="(job, index) in experiences" :key="index" class="timeline-item">
              <div class="timeline-line"></div>
              <span class="date">{{ job.period }}</span>
              <h3 class="role">{{ job.role }}</h3>
              <div class="company">{{ job.company }}</div>
              <ul class="duties">
                <li v-for="(detail, i) in job.details" :key="i">{{ detail }}</li>
              </ul>
            </div>
          </div>
        </div>
        
        <div class="col">
          <h2 class="section-title">Education</h2>
          <div class="education-list">
            <div v-for="(edu, index) in education" :key="index" class="edu-card">
              <div class="edu-date">{{ edu.period }}</div>
              <h3 class="edu-school">{{ edu.school }}</h3>
              <div class="edu-degree">{{ edu.degree }}</div>
            </div>
          </div>
        </div>
      </section>

      <!-- Contact -->
      <footer id="contact" class="footer">
        <div class="footer-card">
          <h2 class="footer-title">Let's work together.</h2>
          <p class="footer-text">Feel free to reach out to discuss your projects.</p>
          <div class="contact-links">
            <a :href="'mailto:' + profile.email" class="contact-btn primary">
              {{ profile.email }}
            </a>
            <a :href="'tel:' + profile.phone" class="contact-btn secondary">
              {{ profile.phone }}
            </a>
            <a :href="profile.linkedin" target="_blank" class="contact-btn secondary">
              LinkedIn ↗
            </a>
          </div>
          <div class="copyright">© 2026 Hubert Touraine</div>
        </div>
      </footer>
    </main>
  </div>
</template>

<style scoped>
/* ---------------------------------
   Theme & Variables
   --------------------------------- */
.app-wrapper {
  min-height: 100vh;
  position: relative;
  overflow-x: hidden;
  color: #fff;
  font-family: 'Inter', sans-serif;
  --primary: #6366f1;
  --primary-glow: rgba(99, 102, 241, 0.4);
  --bg-dark: #0a0a0a;
  --card-bg: rgba(18, 18, 18, 0.8);
  --border: rgba(255, 255, 255, 0.08);
}

/* Background Effects */
.bg-grid {
  position: fixed;
  top: 0; left: 0; width: 100%; height: 100%;
  background-image: 
    linear-gradient(rgba(255, 255, 255, 0.02) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 255, 255, 0.02) 1px, transparent 1px);
  background-size: 40px 40px;
  pointer-events: none;
  z-index: -2;
}
.bg-glow {
  position: fixed;
  top: 50%; left: 50%;
  transform: translate(-50%, -50%);
  width: 1000px; height: 1000px;
  background: radial-gradient(circle, rgba(99, 102, 241, 0.06) 0%, transparent 70%);
  z-index: -1;
  pointer-events: none;
}

/* ---------------------------------
   Layout Utilities
   --------------------------------- */
.container {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 1.5rem;
}
.section {
  margin-bottom: 8rem;
}
.section-title {
  font-size: 2.25rem;
  font-weight: 700;
  margin-bottom: 3rem;
  font-family: 'Outfit', sans-serif;
  letter-spacing: -1px;
}
.highlight {
  color: var(--primary);
}

/* ---------------------------------
   Navigation
   --------------------------------- */
.navbar {
  position: fixed;
  top: 0; width: 100%;
  padding: 1.5rem 0;
  z-index: 50;
  background: linear-gradient(to bottom, #0a0a0a 0%, transparent 100%);
  backdrop-filter: blur(10px);
}
.nav-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.logo {
  font-family: 'Outfit', sans-serif;
  font-weight: 700;
  font-size: 1.5rem;
  color: #fff;
}
.dot { color: var(--primary); }
.nav-links {
  display: flex;
  gap: 2.5rem;
  align-items: center;
}
.nav-links a {
  font-size: 0.9rem;
  color: #a1a1aa;
  font-weight: 500;
  transition: color 0.2s;
}
.nav-links a:hover { color: #fff; }
.btn-contact {
  background: #fff;
  color: #000 !important;
  padding: 0.6rem 1.4rem;
  border-radius: 99px;
  font-weight: 600 !important;
  transition: all 0.2s;
}
.btn-contact:hover { 
  transform: translateY(-2px);
  box-shadow: 0 4px 20px rgba(255,255,255,0.2);
}

/* ---------------------------------
   Hero Section
   --------------------------------- */
.hero {
  padding-top: 12rem;
  padding-bottom: 8rem;
  max-width: 850px;
}
.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  background: rgba(99, 102, 241, 0.1);
  color: #818cf8;
  padding: 0.4rem 1rem;
  border-radius: 99px;
  font-size: 0.85rem;
  margin-bottom: 1.5rem;
  border: 1px solid rgba(99, 102, 241, 0.2);
}
.pulsing-dot {
  width: 8px; height: 8px;
  background: #818cf8;
  border-radius: 50%;
  box-shadow: 0 0 10px #818cf8;
  animation: pulse 2s infinite;
}
@keyframes pulse { 0% { opacity: 1; } 50% { opacity: 0.5; } 100% { opacity: 1; } }

.hero-title {
  font-family: 'Outfit', sans-serif;
  font-size: 4.5rem;
  line-height: 1.05;
  font-weight: 800;
  margin-bottom: 2rem;
  letter-spacing: -3px;
}
.block-gradient {
  display: block;
  background: linear-gradient(to right, #fff, #6366f1);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}
.hero-desc {
  font-size: 1.35rem;
  color: #a1a1aa;
  line-height: 1.6;
  max-width: 650px;
  margin-bottom: 3rem;
}
.tech-stack-hero {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
}
.tech-pill {
  font-size: 0.85rem;
  color: #d4d4d8;
  padding: 0.4rem 0.9rem;
  border-radius: 8px;
  background: rgba(255,255,255,0.03);
  border: 1px solid rgba(255,255,255,0.05);
  font-weight: 500;
}

/* ---------------------------------
   Projects Showcase (Split)
   --------------------------------- */
.projects-showcase {
  margin-top: 4rem;
}

.showcase-container {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: 4rem;
  align-items: start;
}

/* Left Nav */
.showcase-title {
  font-size: 2.5rem;
  font-weight: 800;
  margin-bottom: 4rem;
  font-family: 'Outfit', sans-serif;
}

.nav-items {
  display: flex;
  flex-direction: column;
}

.nav-item-wrapper {
  padding: 2.5rem 0;
  border-top: 1px solid var(--border);
  cursor: pointer;
  transition: all 0.4s ease;
  position: relative;
  opacity: 0.5;
}

.nav-item-wrapper:last-child {
  border-bottom: 1px solid var(--border);
}

.nav-item-wrapper.active {
  opacity: 1;
  padding-left: 1rem;
}

.nav-item-wrapper:hover {
  opacity: 0.8;
}

.nav-item-wrapper.active:hover {
  opacity: 1;
}

.nav-item {
  display: flex;
  align-items: flex-start;
  gap: 2rem;
}

.nav-index {
  font-size: 0.85rem;
  font-weight: 700;
  color: var(--primary);
  margin-top: 0.5rem;
  font-family: 'Outfit', sans-serif;
}

.nav-title {
  font-size: 2.8rem;
  font-weight: 700;
  line-height: 1;
  margin-bottom: 0.5rem;
  font-family: 'Outfit', sans-serif;
  letter-spacing: -1.5px;
}

.nav-subtitle {
  font-size: 0.85rem;
  text-transform: uppercase;
  letter-spacing: 2px;
  color: #71717a;
  font-weight: 600;
}

/* Right Preview */
.project-preview-stage {
  position: sticky;
  top: 15vh;
}

.preview-window {
  background: var(--card-bg);
  border: 1px solid var(--border);
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 40px 100px -20px rgba(0,0,0,0.5);
}

.preview-media-placeholder {
  aspect-ratio: 16/10;
  background: linear-gradient(135deg, #1a1a1a 0%, #0a0a0a 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  border-bottom: 1px solid var(--border);
  overflow: hidden;
}

.preview-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
}

.slider-container {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.slider-controls {
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  transform: translateY(-50%);
  display: flex;
  justify-content: space-between;
  padding: 0 1rem;
  pointer-events: none;
  z-index: 10;
}

.slider-btn {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background: rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  pointer-events: auto;
  transition: all 0.3s ease;
  opacity: 0;
}

.slider-container:hover .slider-btn {
  opacity: 1;
}

.slider-btn:hover {
  background: var(--primary);
  transform: scale(1.1);
}

.slider-dots {
  position: absolute;
  bottom: 1.5rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 0.5rem;
  z-index: 10;
}

.dot-indicator {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.3);
  cursor: pointer;
  transition: all 0.3s ease;
}

.dot-indicator.active {
  background: var(--primary);
  width: 24px;
  border-radius: 4px;
}

/* Slide Transitions */
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all 0.4s ease;
}

.slide-fade-enter-from {
  opacity: 0;
  transform: translateX(30px);
}

.slide-fade-leave-to {
  opacity: 0;
  transform: translateX(-30px);
}

.preview-window:hover .preview-img {
  transform: scale(1.05);
}

.media-inner {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #3f3f46;
}

.placeholder-icon {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

.placeholder-icon span {
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.preview-details {
  padding: 2.5rem;
}

.preview-desc {
  font-size: 1.1rem;
  color: #a1a1aa;
  line-height: 1.6;
  margin-bottom: 2rem;
}

.preview-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

/* Animated Transitions */
.preview-fade-enter-active,
.preview-fade-leave-active {
  transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}

.preview-fade-enter-from {
  opacity: 0;
  transform: translateY(20px) scale(0.98);
}

.preview-fade-leave-to {
  opacity: 0;
  transform: translateY(-20px) scale(0.98);
}

/* Mobile Adjustments for Showcase */
@media (max-width: 900px) {
  .showcase-container {
    grid-template-columns: 1fr;
  }
  .project-preview-stage {
    display: none; /* Hide on small screens for this specific layout type */
  }
  .nav-item-wrapper {
    opacity: 1;
    padding: 2rem 0;
  }
  .nav-title {
    font-size: 2rem;
  }
}

/* ---------------------------------
   Experience & Education
   --------------------------------- */
.split-section {
  display: grid;
  grid-template-columns: 1.2fr 0.8fr;
  gap: 4rem;
}

/* Timeline */
.timeline {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
  position: relative;
  border-left: 1px solid var(--border);
  padding-left: 2rem;
}
.timeline-item {
  position: relative;
}
.timeline-item::before {
  content: '';
  position: absolute;
  left: -2.35rem;
  top: 0.4rem;
  width: 10px; height: 10px;
  background: var(--bg-dark);
  border: 2px solid var(--primary);
  border-radius: 50%;
}
.date {
  font-size: 0.85rem;
  color: #71717a;
  margin-bottom: 0.25rem;
  display: block;
}
.role {
  font-size: 1.2rem;
  margin-bottom: 0.2rem;
}
.company {
  color: #fff;
  font-weight: 500;
  margin-bottom: 0.8rem;
}
.duties {
  list-style: none;
  font-size: 0.95rem;
  color: #a1a1aa;
}
.duties li {
  margin-bottom: 0.5rem;
  position: relative;
  padding-left: 1rem;
}
.duties li::before {
  content: '›';
  position: absolute;
  left: 0;
  color: var(--primary);
}

/* Education Cards */
.education-list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
.edu-card {
  background: var(--card-bg);
  border: 1px solid var(--border);
  padding: 1.5rem;
  border-radius: 12px;
}
.edu-date {
  font-size: 0.8rem;
  color: #71717a;
  margin-bottom: 0.5rem;
}
.edu-school {
  font-size: 1.1rem;
  margin-bottom: 0.25rem;
}
.edu-degree {
  font-size: 0.9rem;
  color: #a1a1aa;
}

/* ---------------------------------
   Footer
   --------------------------------- */
.footer-card {
  background: linear-gradient(180deg, rgba(23,23,23,0.5) 0%, rgba(99,102,241,0.05) 100%);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 4rem 2rem;
  text-align: center;
}
.footer-title {
  font-family: 'Outfit', sans-serif;
  font-size: 2.5rem;
  margin-bottom: 1rem;
}
.footer-text {
  color: #a1a1aa;
  margin-bottom: 2.5rem;
}
.contact-links {
  display: flex;
  justify-content: center;
  gap: 1rem;
  flex-wrap: wrap;
  margin-bottom: 3rem;
}
.contact-btn {
  padding: 0.8rem 1.5rem;
  border-radius: 12px;
  font-weight: 500;
  transition: transform 0.2s, background 0.2s;
}
.contact-btn.primary {
  background: #fff;
  color: #000;
}
.contact-btn.secondary {
  background: rgba(255,255,255,0.05);
  color: #fff;
  border: 1px solid rgba(255,255,255,0.1);
}
.contact-btn:hover {
  transform: translateY(-2px);
}
.copyright {
  font-size: 0.8rem;
  color: #52525b;
}

/* ---------------------------------
   Responsive
   --------------------------------- */
@media (max-width: 768px) {
  .hero-title { font-size: 3rem; }
  .split-section { grid-template-columns: 1fr; gap: 3rem; }
  .nav-links { display: none; }
  .container { padding: 0 1.2rem; }
}
</style>
