<!-- App.vue -->
<template>
  <div id="app">
    <!-- Navigation -->
    <nav class="navbar">
      <div class="nav-container">
        <div class="nav-brand">
          <h2>{{ portfolioData.name }}</h2>
        </div>
        <ul class="nav-menu" :class="{ active: isMenuOpen }">
          <li class="nav-item">
            <a href="#about" class="nav-link" @click="closeMenu">About</a>
          </li>
          <li class="nav-item">
            <a href="#how-built" class="nav-link" @click="closeMenu">How I Built This</a>
          </li>
          <li class="nav-item">
            <a href="#events" class="nav-link" @click="closeMenu">Events</a>
          </li>
          <li class="nav-item">
            <a href="#pr" class="nav-link" @click="closeMenu">PR Activities</a>
          </li>
          <li class="nav-item">
            <a href="#contact" class="nav-link" @click="closeMenu">Contact</a>
          </li>
        </ul>
        <div class="hamburger" :class="{ active: isMenuOpen }" @click="toggleMenu">
          <span class="bar"></span>
          <span class="bar"></span>
          <span class="bar"></span>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <section class="hero">
      <div class="hero-content">
        <h1 class="hero-title">{{ portfolioData.hero.title }}</h1>
        <p class="hero-subtitle">{{ portfolioData.hero.subtitle }}</p>
        <a href="#about" class="cta-button">Explore My Journey</a>
      </div>
      <div class="hero-animation">
        <div class="floating-shapes">
          <div class="shape shape-1"></div>
          <div class="shape shape-2"></div>
          <div class="shape shape-3"></div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="section about-section">
      <div class="container">
        <h2 class="section-title">About Me</h2>
        <div class="about-content">
          <div class="about-text">
            <h3>{{ portfolioData.about.title }}</h3>
            <p>{{ portfolioData.about.description }}</p>
            <div class="skills">
              <h4>Skills & Technologies</h4>
              <div class="skill-tags">
                <span v-for="skill in portfolioData.about.skills" :key="skill" class="skill-tag">
                  {{ skill }}
                </span>
              </div>
            </div>
            <div class="achievements">
              <h4>Key Achievements</h4>
              <ul>
                <li v-for="achievement in portfolioData.about.achievements" :key="achievement">
                  {{ achievement }}
                </li>
              </ul>
            </div>
          </div>
          <div class="about-image">
            <img :src="profileImage" alt="Profile Photo" class="profile-img" />
          </div>
        </div>
      </div>
    </section>

    <!-- How I Built This Section -->
    <section id="how-built" class="section how-built-section">
      <div class="container">
        <h2 class="section-title">How I Built This Portfolio</h2>
        <div class="build-process">
          <div class="tech-stack">
            <h3>Technology Stack</h3>
            <div class="tech-grid">
              <div v-for="tech in portfolioData.buildProcess.techStack" :key="tech.name" class="tech-item">
                <div class="tech-icon">{{ tech.icon }}</div>
                <h4>{{ tech.name }}</h4>
                <p>{{ tech.description }}</p>
              </div>
            </div>
          </div>
          
          <div class="build-steps">
            <h3>Development Process</h3>
            <div class="timeline">
              <div v-for="(step, index) in portfolioData.buildProcess.steps" :key="index" class="timeline-item">
                <div class="timeline-marker">{{ index + 1 }}</div>
                <div class="timeline-content">
                  <h4>{{ step.title }}</h4>
                  <p>{{ step.description }}</p>
                </div>
              </div>
            </div>
          </div>

          <div class="deployment">
            <h3>Deployment & Hosting</h3>
            <p>{{ portfolioData.buildProcess.deployment }}</p>
            <div class="github-link">
              <a href="https://github.com/ahmadkassam-1/e-portfolio" class="button secondary">View Source Code</a>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Events Section -->
    <section id="events" class="section events-section">
      <div class="container">
        <h2 class="section-title">Events & Activities</h2>
        
        <!-- Passive Events -->
        <div class="events-category">
          <h3>Passive Events</h3>
          <div class="events-grid">
            <div v-for="(event, index) in portfolioData.passiveEvents" :key="event.id" class="event-card">
              <div class="event-image">
                <img 
                  :src="index === 0 ? aiImage : cyberImage" 
                  :alt="event.title"
                  class="event-img" 
                />
              </div>
              <div class="event-content">
                <span class="event-type">{{ event.type }}</span>
                <h4>{{ event.title }}</h4>
                <p class="event-date">{{ event.date }}</p>
                <p class="event-summary">{{ event.summary }}</p>
                <div class="event-learnings">
                  <h5>Key Learnings:</h5>
                  <ul>
                    <li v-for="learning in event.learnings" :key="learning">{{ learning }}</li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Active Event -->
        <div class="events-category">
          <h3>Active Event</h3>
          <div class="event-card featured">
            <div class="event-image">
              <img :src="iwinsImage" :alt="portfolioData.activeEvent.title" class="event-img" />
            </div>
            <div class="event-content">
              <span class="event-type">{{ portfolioData.activeEvent.type }}</span>
              <h4>{{ portfolioData.activeEvent.title }}</h4>
              <p class="event-date">{{ portfolioData.activeEvent.date }}</p>
              <p class="event-summary">{{ portfolioData.activeEvent.summary }}</p>
              <div class="event-role">
                <h5>My Role:</h5>
                <p>{{ portfolioData.activeEvent.role }}</p>
              </div>
              <div class="event-impact">
                <h5>Impact & Results:</h5>
                <ul>
                  <li v-for="impact in portfolioData.activeEvent.impact" :key="impact">{{ impact }}</li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

<section id="pr" class="section pr-section">
  <div class="container">
    <h2 class="section-title">PR Activities</h2>
    <div class="pr-grid">
      <div v-for="activity in portfolioData.prActivities" :key="activity.id" class="pr-card">
        <div class="pr-image">
          <img :src="podcastImage" :alt="activity.title" class="event-img" />
        </div>
        <div class="pr-content">
          <span class="pr-type">{{ activity.type }}</span>
          <h3>{{ activity.title }}</h3>
          <p class="pr-date">{{ activity.date }}</p>
          <p class="pr-summary">{{ activity.summary }}</p>
          <div class="pr-details">
            <h4>Production Details:</h4>
            <ul>
              <li><strong>Target Audience:</strong> {{ activity.targetAudience }}</li>
              <li><strong>Platform:</strong> {{ activity.platform }}</li>
              <li><strong>Reach:</strong> {{ activity.reach }}</li>
              <li><strong>Engagement:</strong> {{ activity.engagement }}</li>
            </ul>
          </div>
          <div class="pr-results">
            <h4>Achievements & Impact:</h4>
            <ul>
              <li v-for="result in activity.results" :key="result">{{ result }}</li>
            </ul>
          </div>
          <div class="podcast-link-container">
            <a href="https://creators.spotify.com/pod/show/howest/episodes/Softwareontwikkeling-in-de-zorgsector-met-Tom-DHulster-CGM-e31rl22" target="_blank" class="button podcast-button">
              <span class="podcast-icon">🎧</span> Listen on Spotify
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

    <!-- Contact Section -->
    <section id="contact" class="section contact-section">
      <div class="container">
        <h2 class="section-title">Get In Touch</h2>
        <div class="contact-content">
          <div class="contact-info">
            <h3>Let's Connect!</h3>
            <p>I'm always interested in new opportunities and collaborations.</p>
            <div class="contact-links">
              <a href="mailto:ahmadkassam59@gmail.com" class="contact-link">
                <span class="icon">📧</span>
                <span>Email</span>
              </a>
              <a href="https://be.linkedin.com/in/ahmad-kassam-b57a9b350?trk=people-guest_people_search-card" class="contact-link">
                <span class="icon">💼</span>
                <span>LinkedIn</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="container">
        <p>&copy; 2025 {{ portfolioData.name }}. Built with Vue.js and deployed on Netlify.</p>
      </div>
    </footer>
  </div>
</template>

<script>
import { ref, reactive, onMounted } from 'vue'
import profileImage from './assets/images/profile.png'
import iwinsImage from './assets/images/iwins-team.png'
import aiImage from './assets/images/ai-reality.png'
import cyberImage from './assets/images/cybercommand.png'
import podcastImage from './assets/images/spotify-svgrepo-com.svg'

export default {
  name: 'EPortfolio',
  setup() {
    const isMenuOpen = ref(false)
    const form = reactive({
      name: '',
      email: '',
      message: ''
    })

    // Portfolio data - customize this with your actual information
    const portfolioData = reactive({
      name: "Ahmad Kassam",
      hero: {
        title: "Welcome to My Digital Portfolio",
        subtitle: "Student, Developer, and Future Leader"
      },
      about: {
        title: "Passionate Student & Aspiring Professional",
        description: "I am a dedicated Applied Computer Science student with a passion for technology, innovation, and making a positive impact. Through my studies and various activities, I've developed strong skills in communication, leadership, and technical problem-solving. I believe in continuous learning and growth, always seeking new challenges and opportunities to expand my knowledge and contribute to meaningful projects.",
        skills: [
          "Frontend Development", "Backend Development", "Mobile App Development", 
          "Web Development", "Database Design", "API Development",
          "Project Management", "Team Leadership", "Version Control (Git)", 
          "Problem Solving", "Software Architecture", "DevOps & Deployment"
        ],
        achievements: [
          "Completed multiple successful academic projects",
          "articipated in various university events",
          "Developed strong technical and soft skills",
          "Built this portfolio website from scratch",
          "Actively engaged in PR activities"
        ]
      },
      buildProcess: {
        techStack: [
          {
            name: "Vue.js",
            icon: "⚡",
            description: "Progressive JavaScript framework for building user interfaces"
          },
          {
            name: "CSS3",
            icon: "🎨",
            description: "Modern styling with animations and responsive design"
          },
          {
            name: "Netlify",
            icon: "🚀",
            description: "Fast and reliable hosting platform for deployment"
          },
          {
            name: "Git",
            icon: "📝",
            description: "Version control and collaborative development"
          }
        ],
        steps: [
          {
            title: "Planning & Design",
            description: "Analyzed requirements, created wireframes, and planned the user experience flow"
          },
          {
            title: "Development Setup",
            description: "Set up Vue.js project, configured build tools, and established project structure"
          },
          {
            title: "Component Development",
            description: "Built reusable components for navigation, sections, and interactive elements"
          },
          {
            title: "Content Integration",
            description: "Added portfolio content, implemented responsive design, and optimized performance"
          },
          {
            title: "Testing & Deployment",
            description: "Tested across devices, fixed bugs, and deployed to Netlify with continuous integration"
          }
        ],
        deployment: "This portfolio is deployed on Netlify, providing fast global CDN delivery, automatic HTTPS, and seamless CI/CD integration with Git. The site is optimized for performance and accessibility, ensuring a great user experience across all devices."
      },
      passiveEvents: [
        {
          id: 1,
          image: "aiImage",
          type: "Presentation", 
          title: "AI: the reality behind the hype",
          date: "November 2024",
          summary: "The presentation by Wim Delvaux, a renowned AI expert, explored artificial intelligence and its comprehensive impact on society. Delvaux specializes in AI's societal implications, particularly in education and ethics. The presentation covered AI's definition, evolution from simple tasks to complex analyses, and its current integration across various industries like healthcare, finance, and education.",
          learnings: [
            "AI performs tasks requiring human intelligence: learning, reasoning, problem-solving, and natural language understanding",
            "AI creates personalized learning environments adapting to individual student strengths and weaknesses",
            "Need for ethical frameworks embedded throughout AI development and addressing algorithmic bias",
            "AI automation requires worker adaptation to roles demanding higher-level thinking and reskilling initiatives",
            "Broad community involvement essential for addressing AI concerns and promoting inclusive dialogue"
          ]
        },
        {
          id: 2,
          image: "cyberImage",
          type: "Presentation",
          title: "Belgium's Cyber Command",
          date: "November 2024",
          summary: "Attended an insightful presentation by Lieutenant Colonel Gunther Godefridis about Belgium's Cyber Command, the military's cybersecurity division established in 2022. The presentation covered the Command's mission to protect national digital infrastructure, conduct cyber operations, and defend against hybrid warfare threats targeting Belgium's critical systems and networks.",
          learnings: [
            "Understanding Belgium's Cyber Command role in protecting military networks, weapons systems, and critical infrastructure",
            "Insights into hybrid warfare threats and state-sponsored cyberattacks targeting Belgium's digital sovereignty",
            "Belgium's participation in NATO cyber exercises like Locked Shields and international cooperation frameworks",
            "The importance of public-private partnerships in strengthening national cybersecurity resilience",
            "Career pathways in military cybersecurity including reservist positions and specialized cyber roles"
          ]
        },
      ],
      activeEvent: {
        type: "Hackathon",
        title: "Hack the Future - Exsertus Challenge",
        date: "November 2024",
        summary: "Participated in Belgium's most epic hackathon with teammate Ahmed under the team name 'Iwins'. Competed in the Exsertus challenge, which involved solving coding challenges to develop a working client application. The competition tested programming skills and problem-solving abilities against other student teams in an intensive hackathon environment.",
        role: "Team Developer alongside Ahmed, contributing to coding solutions and technical implementation for the Exsertus challenge",
        impact: [
          "Shared first place with another team in the Exsertus challenge",
          "Selected as one of three teams nominated for the challenge prize",
          "Demonstrated strong collaborative programming skills under time pressure",
          "Gained hands-on experience with real-world coding challenges and client application development",
          "Built valuable networking connections within Belgium's tech and student community"
        ]
      },
     prActivities: [
        {
          id: 1,
          type: "Podcast Production",
          title: "Software Development in the Healthcare Sector: Insights from the Interview with Tom D'Hulster (CGM)",
          date: "February 2025",
          summary: "Co-hosted and produced a comprehensive podcast episode interviewing Tom D'Hulster, a senior software developer at CGM. The podcast explored the challenges of developing medical software, the impact of GDPR on healthcare technology, security measures for patient data protection, and career insights for aspiring software developers in the healthcare sector.",
          targetAudience: "Computer science students, software developers, and professionals interested in healthcare technology",
          platform: "Podcast distribution platforms and digital media channels",
          reach: "Targeted reach within academic and professional tech communities",
          engagement: "Educational content focusing on real-world software development experiences",
          results: [
            "Successfully conducted in-depth interview covering medical software development challenges",
            "Provided valuable insights on GDPR compliance and patient data security",
            "Explored the intersection of AI technology and healthcare software regulations",
            "Delivered practical career advice for software engineering students",
            "Created educational content bridging academic learning with industry practice"
          ]
        }
      ]
    })

    const toggleMenu = () => {
      isMenuOpen.value = !isMenuOpen.value
    }

    const closeMenu = () => {
      isMenuOpen.value = false
    }


    // Smooth scrolling for navigation links
    onMounted(() => {
      const links = document.querySelectorAll('a[href^="#"]')
      links.forEach(link => {
        link.addEventListener('click', (e) => {
          e.preventDefault()
          const target = document.querySelector(link.getAttribute('href'))
          if (target) {
            target.scrollIntoView({ behavior: 'smooth', block: 'start' })
          }
        })
      })

      // Add scroll animations
      const observerOptions = {
        threshold: 0.1,
        rootMargin: '0px 0px -50px 0px'
      }

      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add('animate-in')
          }
        })
      }, observerOptions)

      const sections = document.querySelectorAll('.section')
      sections.forEach(section => observer.observe(section))
    })

    return {
      isMenuOpen,
      form,
      portfolioData,
      toggleMenu,
      closeMenu,
      profileImage,
      iwinsImage,
      aiImage,
      cyberImage,
      podcastImage
    }
  }
}
</script>

<style scoped>
/* CSS Variables */
:root {
  --primary-color: #2563eb;
  --secondary-color: #1e40af;
  --accent-color: #f59e0b;
  --text-primary: #1f2937;
  --text-secondary: #6b7280;
  --bg-primary: #ffffff;
  --bg-secondary: #f9fafb;
  --bg-accent: #eff6ff;
  --border-color: #e5e7eb;
  --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
  --border-radius: 12px;
  --transition: all 0.3s ease;
}

/* Global Styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  line-height: 1.6;
  color: var(--text-primary);
  background-color: var(--bg-primary);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Navigation */
.navbar {
  background: var(--bg-primary);
  box-shadow: var(--shadow);
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 1000;
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 20px;
}

.nav-brand h2 {
  color: var(--primary-color);
  font-weight: 700;
}

.nav-menu {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-item {
  margin-left: 2rem;
}

.nav-link {
  text-decoration: none;
  color: var(--text-primary);
  font-weight: 500;
  transition: var(--transition);
  position: relative;
}

.nav-link:hover {
  color: var(--primary-color);
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -4px;
  left: 0;
  width: 0;
  height: 2px;
  background-color: var(--primary-color);
  transition: var(--transition);
}

.nav-link:hover::after {
  width: 100%;
}

.hamburger {
  display: none;
  flex-direction: column;
  cursor: pointer;
}

.bar {
  width: 25px;
  height: 3px;
  background-color: var(--text-primary);
  margin: 3px 0;
  transition: var(--transition);
}

/* Hero Section */
.hero {
  background: linear-gradient(135deg, var(--bg-accent) 0%, var(--bg-primary) 100%);
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  overflow: hidden;
}

.hero-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  text-align: center;
  z-index: 2;
}

.hero-title {
  font-size: 3.5rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 1rem;
  animation: fadeInUp 1s ease;
}

.hero-subtitle {
  font-size: 1.5rem;
  color: var(--text-secondary);
  margin-bottom: 2rem;
  animation: fadeInUp 1s ease 0.2s both;
}

.cta-button {
  display: inline-block;
  background: var(--primary-color);
  color: white;
  padding: 1rem 2rem;
  border-radius: var(--border-radius);
  text-decoration: none;
  font-weight: 600;
  transition: var(--transition);
  animation: fadeInUp 1s ease 0.4s both;
}

.cta-button:hover {
  background: var(--secondary-color);
  transform: translateY(-2px);
  box-shadow: var(--shadow-lg);
}

/* Floating Shapes Animation */
.hero-animation {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.floating-shapes {
  position: relative;
  width: 100%;
  height: 100%;
}

.shape {
  position: absolute;
  opacity: 0.1;
  animation: float 6s ease-in-out infinite;
}

.shape-1 {
  top: 20%;
  left: 10%;
  width: 60px;
  height: 60px;
  background: var(--primary-color);
  border-radius: 50%;
  animation-delay: 0s;
}

.shape-2 {
  top: 60%;
  right: 10%;
  width: 40px;
  height: 40px;
  background: var(--accent-color);
  border-radius: 10px;
  animation-delay: 2s;
}

.shape-3 {
  bottom: 20%;
  left: 20%;
  width: 80px;
  height: 80px;
  background: var(--secondary-color);
  border-radius: 20px;
  animation-delay: 4s;
}

/* Sections */
.section {
  padding: 5rem 0;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.6s ease;
}

.section.animate-in {
  opacity: 1;
  transform: translateY(0);
}

.section-title {
  font-size: 2.5rem;
  text-align: center;
  margin-bottom: 3rem;
  color: var(--text-primary);
  position: relative;
}

.section-title::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 3px;
  background: var(--primary-color);
}

/* About Section */
.about-section {
  background: var(--bg-secondary);
}

.about-content {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 3rem;
  align-items: center;
}

.about-text h3 {
  font-size: 1.8rem;
  margin-bottom: 1rem;
  color: var(--primary-color);
}

.about-text p {
  font-size: 1.1rem;
  line-height: 1.8;
  color: var(--text-secondary);
  margin-bottom: 2rem;
}

.skills h4,
.achievements h4 {
  margin-bottom: 1rem;
  color: var(--text-primary);
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 2rem;
}

.skill-tag {
  background: var(--primary-color);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.9rem;
  font-weight: 500;
}

.achievements ul {
  list-style: none;
  padding-left: 0;
}

.achievements li {
  position: relative;
  padding-left: 1.5rem;
  margin-bottom: 0.5rem;
  color: var(--text-secondary);
}

.achievements li::before {
  content: '✓';
  position: absolute;
  left: 0;
  color: var(--accent-color);
  font-weight: bold;
}

.about-image {
  display: flex;
  justify-content: center;
}

.profile-img {
  width: 250px;
  height: 250px;
  border-radius: 50%;
  object-fit: cover;
  box-shadow: var(--shadow-lg);
  transition: var(--transition);
  border: 4px solid var(--primary-color);
}

.profile-img:hover {
  transform: scale(1.05);
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.2);
}

.image-placeholder {
  width: 250px;
  height: 250px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: 600;
  box-shadow: var(--shadow-lg);
}

/* How Built Section */
.tech-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-bottom: 3rem;
}

.tech-item {
  background: var(--bg-primary);
  padding: 2rem;
  border-radius: var(--border-radius);
  text-align: center;
  box-shadow: var(--shadow);
  transition: var(--transition);
}

.tech-item:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-lg);
}

.tech-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.tech-item h4 {
  margin-bottom: 1rem;
  color: var(--primary-color);
}

.timeline {
  position: relative;
  padding-left: 2rem;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 10px;
  top: 0;
  bottom: 0;
  width: 2px;
  background: var(--primary-color);
}

.timeline-item {
  position: relative;
  margin-bottom: 2rem;
  padding-bottom: 2rem;
}

.timeline-marker {
  position: absolute;
  left: -35px;
  top: 0;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background: var(--primary-color);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  z-index: 2;
}

.timeline-content h4 {
  color: var(--primary-color);
  margin-bottom: 0.5rem;
}

.deployment {
  background: var(--bg-accent);
  padding: 2rem;
  border-radius: var(--border-radius);
  margin-top: 3rem;
}

.deployment h3 {
  color: var(--primary-color);
  margin-bottom: 1rem;
}

.github-link {
  margin-top: 1rem;
}

/* Events Section */
.events-section {
  background: var(--bg-secondary);
}

.events-category {
  margin-bottom: 4rem;
}

.events-category h3 {
  font-size: 2rem;
  color: var(--primary-color);
  margin-bottom: 2rem;
  border-bottom: 2px solid var(--primary-color);
  padding-bottom: 0.5rem;
}

.events-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 2rem;
}

.event-card {
  background: var(--bg-primary);
  border-radius: var(--border-radius);
  overflow: hidden;
  box-shadow: var(--shadow);
  transition: var(--transition);
}

.event-card:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-lg);
}

.event-card.featured {
  border: 2px solid var(--accent-color);
}

.event-image {
  height: 250px;
  width: 100%;
  overflow: hidden;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

.event-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  transition: var(--transition);
}

/* Specific styling for iwinsImage to prevent top cropping */
.event-card.featured .event-img {
  object-position: center top;
  object-fit: contain;
  background: var(--bg-secondary);
}

.event-img:hover {
  transform: scale(1.02);
}

.event-content {
  padding: 1.5rem;
}

.event-type {
  display: inline-block;
  background: var(--accent-color);
  color: white;
  padding: 0.3rem 0.8rem;
  border-radius: 15px;
  font-size: 0.8rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.event-card h4 {
  font-size: 1.3rem;
  color: var(--primary-color);
  margin-bottom: 0.5rem;
}

.event-date {
  color: var(--text-secondary);
  font-weight: 500;
  margin-bottom: 1rem;
}

.event-summary {
  color: var(--text-secondary);
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.event-learnings,
.event-role,
.event-impact {
  margin-top: 1.5rem;
}

.event-learnings h5,
.event-role h5,
.event-impact h5 {
  color: var(--primary-color);
  margin-bottom: 0.5rem;
}

.event-learnings ul,
.event-impact ul {
  list-style: none;
  padding-left: 0;
}

.event-learnings li,
.event-impact li {
  position: relative;
  padding-left: 1.5rem;
  margin-bottom: 0.5rem;
  color: var(--text-secondary);
}

.event-learnings li::before,
.event-impact li::before {
  content: '•';
  position: absolute;
  left: 0;
  color: var(--accent-color);
  font-weight: bold;
}

.event-role p {
  color: var(--text-secondary);
  font-style: italic;
}

/* PR Section */
.pr-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
  gap: 3rem;
}

.pr-card {
  background: var(--bg-primary);
  border-radius: var(--border-radius);
  overflow: hidden;
  box-shadow: var(--shadow);
  transition: var(--transition);
}

.pr-card:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-lg);
}

.pr-image {
  height: 120px;  /* Make it smaller */
  width: 120px;   /* Set specific width */
  margin: 0 auto; /* Center horizontally */
  overflow: hidden;
  position: relative;
  border-radius: 10px; /* Optional: add rounded corners */
}

.pr-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: var(--transition);
}

.pr-img:hover {
  transform: scale(1.05);
}

.pr-content {
  padding: 2rem;
}

.pr-type {
  display: inline-block;
  background: var(--primary-color);
  color: white;
  padding: 0.3rem 0.8rem;
  border-radius: 15px;
  font-size: 0.8rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.pr-card h3 {
  font-size: 1.5rem;
  color: var(--primary-color);
  margin-bottom: 0.5rem;
}

.pr-date {
  color: var(--text-secondary);
  font-weight: 500;
  margin-bottom: 1rem;
}

.pr-summary {
  color: var(--text-secondary);
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.pr-details,
.pr-results {
  margin-top: 1.5rem;
}

.pr-details h4,
.pr-results h4 {
  color: var(--primary-color);
  margin-bottom: 1rem;
}

.pr-details ul,
.pr-results ul {
  list-style: none;
  padding-left: 0;
}

.pr-details li,
.pr-results li {
  margin-bottom: 0.5rem;
  color: var(--text-secondary);
}

.pr-details li strong {
  color: var(--text-primary);
}

.pr-results li {
  position: relative;
  padding-left: 1.5rem;
}

.pr-results li::before {
  content: '✅';
  position: absolute;
  left: 0;
}

/* Contact Section */
.contact-section {
  background: var(--bg-secondary);
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  align-items: start;
}

.contact-info h3,
.contact-form h3 {
  color: var(--primary-color);
  margin-bottom: 1rem;
}

.contact-info p {
  color: var(--text-secondary);
  margin-bottom: 2rem;
}

.contact-links {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.contact-link {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem;
  background: var(--bg-primary);
  border-radius: var(--border-radius);
  text-decoration: none;
  color: var(--text-primary);
  transition: var(--transition);
  box-shadow: var(--shadow);
}

.contact-link:hover {
  transform: translateX(5px);
  box-shadow: var(--shadow-lg);
}

.contact-link .icon {
  font-size: 1.5rem;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 1rem;
  border: 2px solid var(--border-color);
  border-radius: var(--border-radius);
  font-size: 1rem;
  transition: var(--transition);
  background: var(--bg-primary);
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: var(--primary-color);
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
}

.form-group textarea {
  min-height: 120px;
  resize: vertical;
}

/* Buttons */
.button {
  display: inline-block;
  padding: 1rem 2rem;
  border-radius: var(--border-radius);
  text-decoration: none;
  font-weight: 600;
  transition: var(--transition);
  cursor: pointer;
  border: none;
  font-size: 1rem;
}

.button.primary {
  background: var(--primary-color);
  color: white;
}

.button.primary:hover {
  background: var(--secondary-color);
  transform: translateY(-2px);
  box-shadow: var(--shadow-lg);
}

.button.secondary {
  background: transparent;
  color: var(--primary-color);
  border: 2px solid var(--primary-color);
}

.button.secondary:hover {
  background: var(--primary-color);
  color: white;
}

/* Footer */
.footer {
  background: var(--text-primary);
  color: white;
  text-align: center;
  padding: 2rem 0;
}

.footer p {
  margin: 0;
  opacity: 0.8;
}

/* Animations */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}

/* Responsive Design */
@media (max-width: 1024px) {
  .about-content {
    grid-template-columns: 1fr;
    text-align: center;
  }

  .contact-content {
    grid-template-columns: 1fr;
  }

  .hero-title {
    font-size: 3rem;
  }
}

@media (max-width: 768px) {
  .nav-menu {
    position: fixed;
    left: -100%;
    top: 70px;
    flex-direction: column;
    background-color: var(--bg-primary);
    width: 100%;
    text-align: center;
    transition: var(--transition);
    box-shadow: var(--shadow);
    padding: 2rem 0;
  }

  .nav-menu.active {
    left: 0;
  }

  .nav-item {
    margin: 1rem 0;
  }

  .hamburger {
    display: flex;
  }

  .hamburger.active .bar:nth-child(2) {
    opacity: 0;
  }

  .hamburger.active .bar:nth-child(1) {
    transform: translateY(8px) rotate(45deg);
  }

  .hamburger.active .bar:nth-child(3) {
    transform: translateY(-8px) rotate(-45deg);
  }

  .hero-title {
    font-size: 2.5rem;
  }

  .section-title {
    font-size: 2rem;
  }

  .events-grid {
    grid-template-columns: 1fr;
  }

  .pr-grid {
    grid-template-columns: 1fr;
  }

  .tech-grid {
    grid-template-columns: 1fr;
  }

  .section {
    padding: 3rem 0;
  }

  .timeline {
    padding-left: 1rem;
  }

  .timeline-marker {
    left: -25px;
    width: 25px;
    height: 25px;
    font-size: 0.8rem;
  }
}

.podcast-link-container {
  margin-top: 2rem;
  display: flex;
  justify-content: center;
}

.podcast-button {
  background-color: #1DB954; /* Spotify green */
  color: white;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.8rem 1.5rem;
  border-radius: 30px;
  font-weight: 600;
  transition: all 0.3s ease;
  box-shadow: 0 4px 6px rgba(29, 185, 84, 0.2);
}

.podcast-button:hover {
  background-color: #1ed760; /* Lighter Spotify green on hover */
  transform: translateY(-3px);
  box-shadow: 0 7px 14px rgba(29, 185, 84, 0.3);
}

.podcast-icon {
  font-size: 1.3rem;
}

@media (max-width: 480px) {
  .hero-title {
    font-size: 2rem;
  }

  .hero-subtitle {
    font-size: 1.2rem;
  }

  .container {
    padding: 0 15px;
  }

  .events-grid,
  .pr-grid {
    grid-template-columns: 1fr;
  }

  .event-card,
  .pr-card {
    margin-bottom: 1rem;
  }
}
</style>