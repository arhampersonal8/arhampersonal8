<!DOCTYPE html>
<html lang="en" class="dark scroll-smooth">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Arham Khan | AI & ML Student & Researcher</title>
  
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: {
            brand: {
              pink: '#EF93C4',
              hot: '#FF69B4',
              purple: '#A855F7',
              dark: '#0F172A',
              card: 'rgba(30, 41, 59, 0.7)',
              lightCard: 'rgba(255, 255, 255, 0.85)',
            }
          },
          animation: {
            'pulse-slow': 'pulse 4s cubic-bezier(0.4, 0, 0.6, 1) infinite',
            'float': 'float 6s ease-in-out infinite',
          },
          keyframes: {
            float: {
              '0%, 100%': { transform: 'translateY(0px)' },
              '50%': { transform: 'translateY(-10px)' },
            }
          }
        }
      }
    }
  </script>

  <!-- Google Fonts & Font Awesome Icons -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;600&family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

  <!-- Three.js Library for Animated Live Background -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

  <style>
    body {
      font-family: 'Inter', sans-serif;
      overflow-x: hidden;
    }
    .font-code {
      font-family: 'Fira Code', monospace;
    }
    
    /* Live Canvas Background Layer */
    #bg-canvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      z-index: -10;
      pointer-events: none;
    }

    /* Custom Glassmorphism Effect */
    .glass-panel {
      background: rgba(15, 23, 42, 0.65);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid rgba(239, 147, 196, 0.18);
    }

    .light .glass-panel {
      background: rgba(255, 255, 255, 0.75);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid rgba(239, 147, 196, 0.3);
    }

    /* Glow Border Effect on Hover */
    .glow-hover {
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    }
    .glow-hover:hover {
      box-shadow: 0 0 25px rgba(239, 147, 196, 0.35);
      border-color: rgba(239, 147, 196, 0.6);
      transform: translateY(-3px);
    }

    /* Custom Scrollbar */
    ::-webkit-scrollbar {
      width: 8px;
    }
    ::-webkit-scrollbar-track {
      background: #0f172a;
    }
    ::-webkit-scrollbar-thumb {
      background: #ef93c4;
      border-radius: 4px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #ff69b4;
    }
  </style>
</head>

<body class="bg-slate-950 text-slate-100 dark:bg-slate-950 dark:text-slate-100 transition-colors duration-300 min-h-screen relative selection:bg-brand-pink selection:text-slate-900">

  <!-- Three.js Interactive Live Particle Canvas Background -->
  <canvas id="bg-canvas"></canvas>

  <!-- NAVIGATION BAR -->
  <header class="sticky top-0 z-50 w-full glass-panel border-b border-slate-800/50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
      
      <!-- Brand Logo -->
      <a href="#hero" class="flex items-center space-x-2 group">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-brand-pink to-brand-purple flex items-center justify-center text-slate-950 font-bold text-xl shadow-lg shadow-pink-500/20 group-hover:scale-105 transition-transform">
          AK
        </div>
        <span class="font-bold text-lg tracking-wide text-transparent bg-clip-text bg-gradient-to-r from-brand-pink to-brand-purple">
          Arham Khan
        </span>
      </a>

      <!-- Desktop Nav Navigation -->
      <nav class="hidden md:flex items-center space-x-8 text-sm font-medium">
        <a href="#about" class="hover:text-brand-pink transition-colors">About</a>
        <a href="#skills" class="hover:text-brand-pink transition-colors">Skills & Expertise</a>
        <a href="#projects" class="hover:text-brand-pink transition-colors">Projects</a>
        <a href="#experience" class="hover:text-brand-pink transition-colors">Experience</a>
        <a href="#certifications" class="hover:text-brand-pink transition-colors">Certifications</a>
        <a href="#connect" class="hover:text-brand-pink transition-colors">Contact</a>
      </nav>

      <!-- Action Buttons -->
      <div class="flex items-center space-x-4">
        <!-- Theme Toggle -->
        <button id="theme-toggle" aria-label="Toggle Theme" class="p-2 rounded-lg bg-slate-800/80 hover:bg-slate-700/80 text-brand-pink transition-colors border border-slate-700">
          <i id="theme-icon" class="fas fa-moon text-lg"></i>
        </button>

        <!-- Mobile Menu Toggle Button -->
        <button id="mobile-menu-btn" aria-label="Toggle Navigation Menu" class="md:hidden p-2 rounded-lg bg-slate-800/80 text-slate-200">
          <i class="fas fa-bars text-xl"></i>
        </button>
      </div>
    </div>

    <!-- Mobile Nav Drawer -->
    <div id="mobile-menu" class="hidden md:hidden glass-panel border-b border-slate-800 px-4 pt-2 pb-6 space-y-3">
      <a href="#about" class="block py-2 text-slate-200 hover:text-brand-pink">About</a>
      <a href="#skills" class="block py-2 text-slate-200 hover:text-brand-pink">Skills & Expertise</a>
      <a href="#projects" class="block py-2 text-slate-200 hover:text-brand-pink">Projects</a>
      <a href="#experience" class="block py-2 text-slate-200 hover:text-brand-pink">Experience</a>
      <a href="#certifications" class="block py-2 text-slate-200 hover:text-brand-pink">Certifications</a>
      <a href="#connect" class="block py-2 text-slate-200 hover:text-brand-pink">Contact</a>
    </div>
  </header>

  <!-- MAIN CONTENT CONTAINER -->
  <main class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-10 space-y-20">

    <!-- HERO SECTION -->
    <section id="hero" class="pt-6 pb-12 flex flex-col items-center text-center space-y-8">
      
      <!-- Responsive Animated Header Banner -->
      <div class="w-full max-w-4xl rounded-2xl overflow-hidden shadow-2xl shadow-pink-500/10 border border-brand-pink/30 animate-float">
        <picture>
          <source media="(prefers-color-scheme: dark)" srcset="https://capsule-render.vercel.app/api?type=waving&color=gradient&custom_color_list=24,1&height=220&section=header&text=Welcome%20to%20my%20Space!&fontSize=42&fontColor=EF93C4&animation=twinkling&fontAlignY=38">
          <source media="(prefers-color-scheme: light)" srcset="https://capsule-render.vercel.app/api?type=waving&color=gradient&custom_color_list=1,24&height=220&section=header&text=Welcome%20to%20my%20Space!&fontSize=42&fontColor=FF69B4&animation=twinkling&fontAlignY=38">
          <img src="https://capsule-render.vercel.app/api?type=waving&color=EF93C4&height=220&section=header&text=Welcome%20to%20my%20Space!&fontSize=42&fontColor=fff&animation=twinkling&fontAlignY=38" class="w-full object-cover" alt="Welcome Header Banner" />
        </picture>
      </div>

      <!-- Main Title Heading -->
      <div class="space-y-4">
        <h1 class="text-4xl sm:text-6xl font-extrabold tracking-tight">
          Hey there, I'm <a href="https://github.com/arhampersonal8" target="_blank" class="text-transparent bg-clip-text bg-gradient-to-r from-brand-pink via-purple-400 to-brand-hot hover:underline">Arham Khan</a> 👋
        </h1>
        
        <!-- Live Typing Animation Box -->
        <div class="h-12 flex items-center justify-center">
          <span id="typing-text" class="text-xl sm:text-2xl font-code font-semibold text-brand-pink"></span>
          <span class="animate-pulse text-brand-pink font-code text-2xl">|</span>
        </div>
      </div>

      <!-- Call to Action Buttons -->
      <div class="flex flex-wrap items-center justify-center gap-4 pt-2">
        <a href="#projects" class="px-7 py-3 rounded-xl bg-gradient-to-r from-brand-pink to-brand-hot text-slate-950 font-bold shadow-lg shadow-pink-500/25 hover:opacity-90 hover:scale-105 transition-all">
          <i class="fas fa-rocket mr-2"></i> Explore Projects
        </a>
        <a href="mailto:arhampersonal8@gmail.com" class="px-7 py-3 rounded-xl glass-panel text-slate-100 font-semibold border border-brand-pink/40 hover:bg-brand-pink/20 hover:scale-105 transition-all">
          <i class="fas fa-envelope mr-2 text-brand-pink"></i> Get In Touch
        </a>
        <a href="https://github.com/arhampersonal8" target="_blank" class="p-3 rounded-xl glass-panel text-slate-200 border border-slate-700 hover:text-brand-pink hover:scale-110 transition-all" title="GitHub Profile">
          <i class="fab fa-github text-xl"></i>
        </a>
      </div>
    </section>

    <!-- ABOUT ME SECTION -->
    <section id="about" class="glass-panel p-6 sm:p-10 rounded-3xl space-y-8 glow-hover">
      <div class="text-center space-y-2">
        <span class="text-brand-pink font-semibold tracking-wider text-sm uppercase">Background & Focus</span>
        <h2 class="text-3xl sm:text-4xl font-bold flex items-center justify-center gap-3">
          <span>🌸</span> About Me
        </h2>
        <div class="w-16 h-1 bg-gradient-to-r from-brand-pink to-brand-purple mx-auto rounded-full"></div>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 items-stretch">
        <!-- Main Description -->
        <div class="md:col-span-2 space-y-4 text-slate-300 leading-relaxed text-base sm:text-lg">
          <p>
            As an aspiring student in <strong class="text-brand-pink">Artificial Intelligence and Machine Learning</strong> with a strong interest in AI/ML research, applied machine learning, and building intelligent systems for real-world problems. I enjoy understanding how things work, experimenting with new ideas, and turning complex problems into practical, user-centric technical solutions.
          </p>
          <p>
            I’m particularly interested in research that connects AI with meaningful challenges, especially in areas such as <span class="text-slate-100 font-medium">healthcare, smart energy systems, and socially impactful technologies</span>.
          </p>
          <div class="p-4 rounded-xl bg-slate-900/60 border border-brand-pink/20 flex items-start gap-3">
            <i class="fas fa-bullseye text-2xl text-brand-pink mt-1"></i>
            <div>
              <h4 class="font-semibold text-slate-100">My Ultimate Goal</h4>
              <p class="text-sm text-slate-400">To grow as a pioneering AI/ML researcher & engineer, contributing to systems and publications that deliver measurable real-world impact.</p>
            </div>
          </div>
        </div>

        <!-- Exploration Cards Sidebar -->
        <div class="space-y-4">
          <div class="p-5 rounded-2xl bg-slate-900/80 border border-slate-800">
            <h3 class="font-bold text-lg text-brand-pink mb-3 flex items-center gap-2">
              <i class="fas fa-book-open"></i> Currently Exploring
            </h3>
            <ul class="space-y-2 text-sm text-slate-300">
              <li class="flex items-center gap-2"><i class="fas fa-check-circle text-xs text-brand-pink"></i> Deep Learning & Neural Nets</li>
              <li class="flex items-center gap-2"><i class="fas fa-check-circle text-xs text-brand-pink"></i> Privacy-Preserving Federated AI</li>
              <li class="flex items-center gap-2"><i class="fas fa-check-circle text-xs text-brand-pink"></i> Multimodal AI & Interaction</li>
              <li class="flex items-center gap-2"><i class="fas fa-check-circle text-xs text-brand-pink"></i> Statistical Methods & Data Science</li>
              <li class="flex items-center gap-2"><i class="fas fa-check-circle text-xs text-brand-pink"></i> Scientific Communication</li>
            </ul>
          </div>

          <div class="p-5 rounded-2xl bg-slate-900/80 border border-slate-800">
            <h3 class="font-bold text-lg text-brand-purple mb-2 flex items-center gap-2">
              <i class="fas fa-microphone"></i> Speaking & Writing
            </h3>
            <p class="text-xs text-slate-300 leading-relaxed">
              I am an active public speaker and scientific communicator who believes explaining complex concepts clearly is just as critical as writing clean code.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- TECH STACK & TOOLS SECTION -->
    <section id="skills" class="space-y-8">
      <div class="text-center space-y-2">
        <span class="text-brand-pink font-semibold tracking-wider text-sm uppercase">Technical Arsenal</span>
        <h2 class="text-3xl sm:text-4xl font-bold">🛠️ Tech Stack & Skillsets</h2>
        <div class="w-16 h-1 bg-gradient-to-r from-brand-pink to-brand-purple mx-auto rounded-full"></div>
      </div>

      <!-- Category Dynamic Cards Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        
        <!-- Programming Languages -->
        <div class="glass-panel p-6 rounded-2xl glow-hover space-y-4">
          <div class="flex items-center justify-between">
            <h3 class="text-xl font-bold flex items-center gap-2">
              <i class="fas fa-code text-brand-pink"></i> Programming Languages
            </h3>
          </div>
          <div class="flex flex-wrap gap-3 pt-2">
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=py" class="w-6 h-6" alt="Python"/> Python
            </span>
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=cpp" class="w-6 h-6" alt="C++"/> C++
            </span>
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=js" class="w-6 h-6" alt="JS"/> JavaScript
            </span>
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=matlab" class="w-6 h-6" alt="MATLAB"/> MATLAB
            </span>
          </div>
        </div>

        <!-- AI / ML & Data Science -->
        <div class="glass-panel p-6 rounded-2xl glow-hover space-y-4">
          <div class="flex items-center justify-between">
            <h3 class="text-xl font-bold flex items-center gap-2">
              <i class="fas fa-brain text-brand-purple"></i> AI / ML & Data Science
            </h3>
          </div>
          <div class="flex flex-wrap gap-3 pt-2">
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=pytorch" class="w-6 h-6" alt="PyTorch"/> PyTorch
            </span>
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=tensorflow" class="w-6 h-6" alt="TensorFlow"/> TensorFlow
            </span>
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=scikitlearn" class="w-6 h-6" alt="Scikit-Learn"/> Scikit-Learn
            </span>
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=pandas" class="w-6 h-6" alt="Pandas"/> Pandas
            </span>
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=numpy" class="w-6 h-6" alt="NumPy"/> NumPy
            </span>
          </div>
        </div>

        <!-- Web Development -->
        <div class="glass-panel p-6 rounded-2xl glow-hover space-y-4">
          <div class="flex items-center justify-between">
            <h3 class="text-xl font-bold flex items-center gap-2">
              <i class="fas fa-globe text-brand-pink"></i> Web Development
            </h3>
          </div>
          <div class="flex flex-wrap gap-3 pt-2">
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=react" class="w-6 h-6" alt="React"/> React
            </span>
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=nodejs" class="w-6 h-6" alt="NodeJS"/> Node.js
            </span>
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=express" class="w-6 h-6" alt="Express"/> Express
            </span>
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=mongodb" class="w-6 h-6" alt="MongoDB"/> MongoDB
            </span>
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=mysql" class="w-6 h-6" alt="MySQL"/> MySQL
            </span>
          </div>
        </div>

        <!-- Developer Tools & Environment -->
        <div class="glass-panel p-6 rounded-2xl glow-hover space-y-4">
          <div class="flex items-center justify-between">
            <h3 class="text-xl font-bold flex items-center gap-2">
              <i class="fas fa-tools text-brand-purple"></i> Tools & Environment
            </h3>
          </div>
          <div class="flex flex-wrap gap-3 pt-2">
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=git" class="w-6 h-6" alt="Git"/> Git
            </span>
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=github" class="w-6 h-6" alt="GitHub"/> GitHub
            </span>
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=vscode" class="w-6 h-6" alt="VSCode"/> VS Code
            </span>
            <span class="px-3 py-2 rounded-xl bg-slate-900/90 border border-slate-700 flex items-center gap-2 text-sm font-medium">
              <img src="https://skillicons.dev/icons?i=figma" class="w-6 h-6" alt="Figma"/> Figma
            </span>
          </div>
        </div>

      </div>

      <!-- AI/ML EXPERTISE TABLE & Breakdown -->
      <div class="glass-panel p-6 sm:p-8 rounded-3xl space-y-6 glow-hover mt-8">
        <h3 class="text-2xl font-bold text-center flex items-center justify-center gap-2">
          <span>🌟</span> AI / ML Expertise Matrix
        </h3>

        <div class="overflow-x-auto">
          <table class="w-full text-left border-collapse">
            <thead>
              <tr class="border-b border-slate-700 text-brand-pink text-sm uppercase">
                <th class="py-3 px-4">Domain</th>
                <th class="py-3 px-4">Proficiency</th>
                <th class="py-3 px-4">Details & Specialization</th>
              </tr>
            </thead>
            <tbody class="divide-y divide-slate-800 text-sm sm:text-base">
              <tr class="hover:bg-slate-900/40 transition-colors">
                <td class="py-4 px-4 font-bold text-slate-100 whitespace-nowrap">Machine Learning</td>
                <td class="py-4 px-4 text-amber-400 whitespace-nowrap">⭐⭐⭐⭐⭐</td>
                <td class="py-4 px-4 text-slate-300">Supervised/Unsupervised learning, Feature Engineering, Model Training, Scikit-learn, Anomaly Detection.</td>
              </tr>
              <tr class="hover:bg-slate-900/40 transition-colors">
                <td class="py-4 px-4 font-bold text-slate-100 whitespace-nowrap">Deep Learning & Vision</td>
                <td class="py-4 px-4 text-amber-400 whitespace-nowrap">⭐⭐⭐⭐☆</td>
                <td class="py-4 px-4 text-slate-300">Neural Networks, PyTorch, TensorFlow, Computer Vision, Emotion & Sentiment Analysis, Multimodal AI.</td>
              </tr>
              <tr class="hover:bg-slate-900/40 transition-colors">
                <td class="py-4 px-4 font-bold text-slate-100 whitespace-nowrap">Federated Learning</td>
                <td class="py-4 px-4 text-amber-400 whitespace-nowrap">⭐⭐⭐⭐☆</td>
                <td class="py-4 px-4 text-slate-300">Privacy-preserving AI, Decentralized training with FedAvg, Smart Grid simulations, Privacy-accuracy trade-offs.</td>
              </tr>
              <tr class="hover:bg-slate-900/40 transition-colors">
                <td class="py-4 px-4 font-bold text-slate-100 whitespace-nowrap">Natural Language Processing</td>
                <td class="py-4 px-4 text-amber-400 whitespace-nowrap">⭐⭐⭐⭐☆</td>
                <td class="py-4 px-4 text-slate-300">Text Analysis, Pretrained Transformer Models, Speech Analysis, Voice-assisted Multimodal Interfaces.</td>
              </tr>
              <tr class="hover:bg-slate-900/40 transition-colors">
                <td class="py-4 px-4 font-bold text-slate-100 whitespace-nowrap">Data Analytics & Stats</td>
                <td class="py-4 px-4 text-amber-400 whitespace-nowrap">⭐⭐⭐⭐⭐</td>
                <td class="py-4 px-4 text-slate-300">Pandas, NumPy, Statistical Modeling, Interactive Dashboards, Plotly, Data Annotation & Pattern Recognition.</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </section>

    <!-- FEATURED PROJECTS SECTION -->
    <section id="projects" class="space-y-8">
      <div class="text-center space-y-2">
        <span class="text-brand-pink font-semibold tracking-wider text-sm uppercase">Innovations & Implementations</span>
        <h2 class="text-3xl sm:text-4xl font-bold">🚀 Featured Projects</h2>
        <div class="w-16 h-1 bg-gradient-to-r from-brand-pink to-brand-purple mx-auto rounded-full"></div>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        
        <!-- Project 1: REMINIPlay -->
        <div class="glass-panel rounded-2xl p-6 glow-hover flex flex-col justify-between space-y-4">
          <div class="space-y-3">
            <div class="flex items-center justify-between">
              <span class="p-3 rounded-xl bg-pink-500/10 text-brand-pink text-2xl"><i class="fas fa-gamepad"></i></span>
              <span class="text-xs font-code px-2 py-1 rounded bg-slate-800 text-slate-400">Healthcare / AI</span>
            </div>
            <h3 class="text-xl font-bold text-slate-100">REMINIPlay</h3>
            <p class="text-xs font-semibold text-brand-pink">Cognitive Gaming & Memory Assistance Platform</p>
            <p class="text-sm text-slate-300 leading-relaxed">
              Developed interactive cognitive games targeting memory improvement, attention, and object recognition for Dementia patients. Integrated AI/ML adaptive difficulty mechanisms, voice assistance, multilingual interfaces, and daily activity reminders.
            </p>
          </div>
          <div class="pt-2 border-t border-slate-800 flex flex-wrap gap-2 text-xs">
            <span class="px-2 py-1 rounded bg-slate-900 border border-slate-800 text-slate-300">Adaptive AI</span>
            <span class="px-2 py-1 rounded bg-slate-900 border border-slate-800 text-slate-300">Voice Assistant</span>
            <span class="px-2 py-1 rounded bg-slate-900 border border-slate-800 text-slate-300">Healthcare</span>
          </div>
        </div>

        <!-- Project 2: Adaptive Sense -->
        <div class="glass-panel rounded-2xl p-6 glow-hover flex flex-col justify-between space-y-4">
          <div class="space-y-3">
            <div class="flex items-center justify-between">
              <span class="p-3 rounded-xl bg-purple-500/10 text-brand-purple text-2xl"><i class="fas fa-robot"></i></span>
              <span class="text-xs font-code px-2 py-1 rounded bg-slate-800 text-slate-400">Multimodal AI</span>
            </div>
            <h3 class="text-xl font-bold text-slate-100">Adaptive Sense</h3>
            <p class="text-xs font-semibold text-brand-purple">Human-AI Interaction System</p>
            <p class="text-sm text-slate-300 leading-relaxed">
              An interactive multimodal AI platform integrating text, speech, image, and video analysis. Features real-time emotion and sentiment detection with confidence-aware predictions, dynamically adjusting UI guidance and interaction complexity.
            </p>
          </div>
          <div class="pt-2 border-t border-slate-800 flex flex-wrap gap-2 text-xs">
            <span class="px-2 py-1 rounded bg-slate-900 border border-slate-800 text-slate-300">Computer Vision</span>
            <span class="px-2 py-1 rounded bg-slate-900 border border-slate-800 text-slate-300">NLP</span>
            <span class="px-2 py-1 rounded bg-slate-900 border border-slate-800 text-slate-300">PyTorch</span>
          </div>
        </div>

        <!-- Project 3: FedGrid -->
        <div class="glass-panel rounded-2xl p-6 glow-hover flex flex-col justify-between space-y-4">
          <div class="space-y-3">
            <div class="flex items-center justify-between">
              <span class="p-3 rounded-xl bg-amber-500/10 text-amber-400 text-2xl"><i class="fas fa-bolt"></i></span>
              <span class="text-xs font-code px-2 py-1 rounded bg-slate-800 text-slate-400">Federated Learning</span>
            </div>
            <h3 class="text-xl font-bold text-slate-100">FedGrid</h3>
            <p class="text-xs font-semibold text-amber-400">Privacy-Preserving Smart Energy Analytics</p>
            <p class="text-sm text-slate-300 leading-relaxed">
              Decentralized energy demand prediction platform using Federated Learning (FedAvg) with Scikit-learn and Pandas. Features anomaly detection via Isolation Forest and interactive Plotly dashboards evaluating privacy vs. accuracy trade-offs.
            </p>
          </div>
          <div class="pt-2 border-t border-slate-800 flex flex-wrap gap-2 text-xs">
            <span class="px-2 py-1 rounded bg-slate-900 border border-slate-800 text-slate-300">FedAvg</span>
            <span class="px-2 py-1 rounded bg-slate-900 border border-slate-800 text-slate-300">Plotly</span>
            <span class="px-2 py-1 rounded bg-slate-900 border border-slate-800 text-slate-300">Smart Grid</span>
          </div>
        </div>

        <!-- Project 4: EZYTable -->
        <div class="glass-panel rounded-2xl p-6 glow-hover flex flex-col justify-between space-y-4">
          <div class="space-y-3">
            <div class="flex items-center justify-between">
              <span class="p-3 rounded-xl bg-blue-500/10 text-blue-400 text-2xl"><i class="fas fa-calendar-alt"></i></span>
              <span class="text-xs font-code px-2 py-1 rounded bg-slate-800 text-slate-400">Optimization</span>
            </div>
            <h3 class="text-xl font-bold text-slate-100">EZYTable</h3>
            <p class="text-xs font-semibold text-blue-400">Automated Timetable Scheduling System</p>
            <p class="text-sm text-slate-300 leading-relaxed">
              Automated scheduling algorithm modeling real-world academic constraints (teachers, rooms, time slots) as a computational optimization problem to completely eliminate manual scheduling conflicts.
            </p>
          </div>
          <div class="pt-2 border-t border-slate-800 flex flex-wrap gap-2 text-xs">
            <span class="px-2 py-1 rounded bg-slate-900 border border-slate-800 text-slate-300">Algorithm</span>
            <span class="px-2 py-1 rounded bg-slate-900 border border-slate-800 text-slate-300">Optimization</span>
            <span class="px-2 py-1 rounded bg-slate-900 border border-slate-800 text-slate-300">Python</span>
          </div>
        </div>

        <!-- Project 5: Aurastic -->
        <div class="glass-panel rounded-2xl p-6 glow-hover flex flex-col justify-between space-y-4 md:col-span-2 lg:col-span-1">
          <div class="space-y-3">
            <div class="flex items-center justify-between">
              <span class="p-3 rounded-xl bg-emerald-500/10 text-emerald-400 text-2xl"><i class="fas fa-handshake"></i></span>
              <span class="text-xs font-code px-2 py-1 rounded bg-slate-800 text-slate-400">Web Platform</span>
            </div>
            <h3 class="text-xl font-bold text-slate-100">Aurastic</h3>
            <p class="text-xs font-semibold text-emerald-400">Skilled Worker-Customer Platform</p>
            <p class="text-sm text-slate-300 leading-relaxed">
              A digital platform designed to bridge local skilled/blue-collar workers with customers, streamlining service discovery, scheduling, and direct transparent communication.
            </p>
          </div>
          <div class="pt-2 border-t border-slate-800 flex flex-wrap gap-2 text-xs">
            <span class="px-2 py-1 rounded bg-slate-900 border border-slate-800 text-slate-300">Full Stack</span>
            <span class="px-2 py-1 rounded bg-slate-900 border border-slate-800 text-slate-300">Service Discovery</span>
            <span class="px-2 py-1 rounded bg-slate-900 border border-slate-800 text-slate-300">Web</span>
          </div>
        </div>

      </div>
    </section>

    <!-- EXPERIENCE & RESEARCH TIMELINE SECTION -->
    <section id="experience" class="space-y-8">
      <div class="text-center space-y-2">
        <span class="text-brand-pink font-semibold tracking-wider text-sm uppercase">Career & Research</span>
        <h2 class="text-3xl sm:text-4xl font-bold">💼 Experience & Research Work</h2>
        <div class="w-16 h-1 bg-gradient-to-r from-brand-pink to-brand-purple mx-auto rounded-full"></div>
      </div>

      <div class="relative border-l-2 border-brand-pink/30 ml-4 md:ml-32 space-y-10 pl-6">

        <!-- Timeline item 1 -->
        <div class="relative group">
          <div class="absolute -left-[31px] top-1.5 w-4 h-4 rounded-full bg-brand-pink border-4 border-slate-950 group-hover:scale-125 transition-transform"></div>
          <div class="glass-panel p-6 rounded-2xl space-y-2 glow-hover">
            <span class="text-xs font-code font-semibold px-3 py-1 rounded-full bg-brand-pink/20 text-brand-pink">Sole Author & Presenter</span>
            <h3 class="text-xl font-bold text-slate-100 mt-2">Research Paper Presentation — College Research Competition</h3>
            <p class="text-sm text-brand-purple font-medium">Title: Fraud Detection in Government Examinations using Machine Learning</p>
            <p class="text-sm text-slate-300 leading-relaxed pt-1">
              Investigated ML frameworks to identify fraudulent patterns and anomalous behaviors in high-stakes examination processes. Formulated the problem, trained ML proof-of-concept models, and presented technical findings independently.
            </p>
          </div>
        </div>

        <!-- Timeline item 2 -->
        <div class="relative group">
          <div class="absolute -left-[31px] top-1.5 w-4 h-4 rounded-full bg-brand-purple border-4 border-slate-950 group-hover:scale-125 transition-transform"></div>
          <div class="glass-panel p-6 rounded-2xl space-y-2 glow-hover">
            <div class="flex flex-wrap justify-between items-center gap-2">
              <span class="text-xs font-code font-semibold px-3 py-1 rounded-full bg-purple-500/20 text-brand-purple">Internship</span>
              <span class="text-xs text-slate-400 font-code"><i class="far fa-calendar-alt mr-1"></i>08/2025 – 11/2025</span>
            </div>
            <h3 class="text-xl font-bold text-slate-100">Research & Content Intern — Entrepreneur Woods</h3>
            <p class="text-sm text-slate-300 leading-relaxed pt-1">
              Conducted secondary market and competitor research across startups and emerging business trends. Synthesized technical insights into structured content and collaborated with cross-functional teams to support client strategy.
            </p>
          </div>
        </div>

        <!-- Timeline item 3 -->
        <div class="relative group">
          <div class="absolute -left-[31px] top-1.5 w-4 h-4 rounded-full bg-amber-400 border-4 border-slate-950 group-hover:scale-125 transition-transform"></div>
          <div class="glass-panel p-6 rounded-2xl space-y-2 glow-hover">
            <div class="flex flex-wrap justify-between items-center gap-2">
              <span class="text-xs font-code font-semibold px-3 py-1 rounded-full bg-amber-500/20 text-amber-400">Research Volunteer</span>
              <span class="text-xs text-slate-400 font-code"><i class="far fa-calendar-alt mr-1"></i>2026</span>
            </div>
            <h3 class="text-xl font-bold text-slate-100">Citizen Science Volunteer — Zooniverse</h3>
            <p class="text-sm text-slate-300 leading-relaxed pt-1">
              Contributed to astronomical research projects involving space-telescope image classification, galaxy morphology analysis, and imaging artifact identification to assist ongoing astrophysics research.
            </p>
          </div>
        </div>

      </div>
    </section>

    <!-- CERTIFICATIONS & ACHIEVEMENTS SECTION -->
    <section id="certifications" class="space-y-8">
      <div class="text-center space-y-2">
        <span class="text-brand-pink font-semibold tracking-wider text-sm uppercase">Milestones & Qualifications</span>
        <h2 class="text-3xl sm:text-4xl font-bold">📜 Certifications & Achievements</h2>
        <div class="w-16 h-1 bg-gradient-to-r from-brand-pink to-brand-purple mx-auto rounded-full"></div>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
        
        <div class="glass-panel p-5 rounded-2xl text-center space-y-2 glow-hover flex flex-col items-center justify-center">
          <span class="text-3xl text-brand-pink mb-1"><i class="fas fa-graduation-cap"></i></span>
          <h4 class="font-bold text-slate-100 text-sm">Research Methods & Evidence Synthesis</h4>
          <span class="text-xs text-slate-400 font-code">DiracLabs</span>
        </div>

        <div class="glass-panel p-5 rounded-2xl text-center space-y-2 glow-hover flex flex-col items-center justify-center">
          <span class="text-3xl text-amber-400 mb-1"><i class="fas fa-trophy"></i></span>
          <h4 class="font-bold text-slate-100 text-sm">PaperSprint 2026 Research Presentation</h4>
          <span class="text-xs text-slate-400 font-code">LNCT&S</span>
        </div>

        <div class="glass-panel p-5 rounded-2xl text-center space-y-2 glow-hover flex flex-col items-center justify-center">
          <span class="text-3xl text-brand-purple mb-1"><i class="fas fa-chart-bar"></i></span>
          <h4 class="font-bold text-slate-100 text-sm">Data Analytics Essentials</h4>
          <span class="text-xs text-slate-400 font-code">Cisco</span>
        </div>

        <div class="glass-panel p-5 rounded-2xl text-center space-y-2 glow-hover flex flex-col items-center justify-center">
          <span class="text-3xl text-blue-400 mb-1"><i class="fas fa-handshake"></i></span>
          <h4 class="font-bold text-slate-100 text-sm">Partnering with AI in Workplace</h4>
          <span class="text-xs text-slate-400 font-code">Forage</span>
        </div>

        <div class="glass-panel p-5 rounded-2xl text-center space-y-2 glow-hover flex flex-col items-center justify-center">
          <span class="text-3xl text-emerald-400 mb-1"><i class="fas fa-briefcase"></i></span>
          <h4 class="font-bold text-slate-100 text-sm">Data Analytics Job Simulation</h4>
          <span class="text-xs text-slate-400 font-code">Deloitte</span>
        </div>

        <div class="glass-panel p-5 rounded-2xl text-center space-y-2 glow-hover flex flex-col items-center justify-center">
          <span class="text-3xl text-yellow-400 mb-1"><i class="fab fa-python"></i></span>
          <h4 class="font-bold text-slate-100 text-sm">Python Essentials 1</h4>
          <span class="text-xs text-slate-400 font-code">Cisco</span>
        </div>

        <div class="glass-panel p-5 rounded-2xl text-center space-y-2 glow-hover flex flex-col items-center justify-center">
          <span class="text-3xl text-rose-400 mb-1"><i class="fas fa-shield-alt"></i></span>
          <h4 class="font-bold text-slate-100 text-sm">Cybersecurity Awareness</h4>
          <span class="text-xs text-slate-400 font-code">HP LIFE</span>
        </div>

        <div class="glass-panel p-5 rounded-2xl text-center space-y-2 glow-hover flex flex-col items-center justify-center">
          <span class="text-3xl text-red-500 mb-1"><i class="fas fa-rocket"></i></span>
          <h4 class="font-bold text-slate-100 text-sm">Adobe University Hackathon</h4>
          <span class="text-xs text-slate-400 font-code">2026</span>
        </div>

      </div>
    </section>

    <!-- CONNECT / SOCIAL CONTACT SECTION -->
    <section id="connect" class="glass-panel p-8 sm:p-12 rounded-3xl text-center space-y-8 glow-hover">
      <div class="space-y-2">
        <span class="text-brand-pink font-semibold tracking-wider text-sm uppercase">Get In Touch</span>
        <h2 class="text-3xl sm:text-4xl font-bold">📫 Connect With Me</h2>
        <p class="text-slate-300 max-w-xl mx-auto text-sm sm:text-base">
          Whether you want to discuss AI research, collaborate on a multimodal project, or just say hello, feel free to reach out through any of these platforms!
        </p>
      </div>

      <!-- Social Badges Row -->
      <div class="flex flex-wrap justify-center items-center gap-4 pt-2">
        
        <a href="https://linkedin.com/in/arhampersonal8" target="_blank" class="px-5 py-3 rounded-xl bg-[#0A66C2]/20 border border-[#0A66C2]/40 text-white font-medium hover:bg-[#0A66C2] hover:scale-105 transition-all flex items-center gap-2">
          <i class="fab fa-linkedin text-xl"></i> LinkedIn
        </a>

        <a href="https://x.com/arhampersonal8" target="_blank" class="px-5 py-3 rounded-xl bg-slate-800 border border-slate-700 text-white font-medium hover:bg-black hover:scale-105 transition-all flex items-center gap-2">
          <i class="fab fa-x-twitter text-xl"></i> Twitter / X
        </a>

        <a href="https://instagram.com/arhampersonal8" target="_blank" class="px-5 py-3 rounded-xl bg-[#E4405F]/20 border border-[#E4405F]/40 text-white font-medium hover:bg-[#E4405F] hover:scale-105 transition-all flex items-center gap-2">
          <i class="fab fa-instagram text-xl"></i> Instagram
        </a>

        <a href="https://tiktok.com/@arhampersonal8" target="_blank" class="px-5 py-3 rounded-xl bg-slate-900 border border-slate-700 text-white font-medium hover:bg-slate-800 hover:scale-105 transition-all flex items-center gap-2">
          <i class="fab fa-tiktok text-xl"></i> TikTok
        </a>

        <a href="https://youtube.com/@arhampersonal8" target="_blank" class="px-5 py-3 rounded-xl bg-[#FF0000]/20 border border-[#FF0000]/40 text-white font-medium hover:bg-[#FF0000] hover:scale-105 transition-all flex items-center gap-2">
          <i class="fab fa-youtube text-xl"></i> YouTube
        </a>

        <a href="mailto:arhampersonal8@gmail.com" class="px-5 py-3 rounded-xl bg-gradient-to-r from-brand-pink to-brand-hot text-slate-950 font-bold hover:scale-105 transition-all flex items-center gap-2 shadow-lg shadow-pink-500/20">
          <i class="fas fa-envelope text-xl"></i> Email Me
        </a>

      </div>
    </section>

  </main>

  <!-- FOOTER SECTION -->
  <footer class="mt-20 border-t border-slate-800/80 glass-panel">
    <div class="max-w-6xl mx-auto px-4 py-8 flex flex-col sm:flex-row items-center justify-between gap-4 text-slate-400 text-sm">
      <p>© 2026 Arham Khan. All rights reserved.</p>
      <div class="flex items-center space-x-6">
        <a href="#hero" class="hover:text-brand-pink transition-colors">Back to top <i class="fas fa-arrow-up ml-1"></i></a>
      </div>
    </div>
    <!-- Footer Decorative Banner Simulation -->
    <div class="w-full overflow-hidden opacity-80">
      <img src="https://capsule-render.vercel.app/api?type=waving&color=EF93C4&height=120&section=footer" class="w-full object-cover h-20" alt="Footer Banner" />
    </div>
  </footer>

  <!-- SCRIPT LOGIC: Interactive Features, Canvas AI Network, Typing Animation -->
  <script>
    // 1. DYNAMIC TYPING ANIMATION
    const typingLines = [
      "AI & Machine Learning Student",
      "Federated Learning & Deep Learning",
      "Building Multimodal AI Systems",
      "Research Enthusiast & Technical Writer"
    ];
    let lineIdx = 0;
    let charIdx = 0;
    let isDeleting = false;
    const typingElement = document.getElementById('typing-text');

    function typeEffect() {
      const currentLine = typingLines[lineIdx];
      if (isDeleting) {
        typingElement.textContent = currentLine.substring(0, charIdx - 1);
        charIdx--;
      } else {
        typingElement.textContent = currentLine.substring(0, charIdx + 1);
        charIdx++;
      }

      let speed = isDeleting ? 40 : 80;

      if (!isDeleting && charIdx === currentLine.length) {
        speed = 2200; // Pause at full word
        isDeleting = true;
      } else if (isDeleting && charIdx === 0) {
        isDeleting = false;
        lineIdx = (lineIdx + 1) % typingLines.length;
        speed = 500;
      }

      setTimeout(typeEffect, speed);
    }
    document.addEventListener('DOMContentLoaded', typeEffect);

    // 2. MOBILE MENU TOGGLE
    const mobileBtn = document.getElementById('mobile-menu-btn');
    const mobileMenu = document.getElementById('mobile-menu');
    mobileBtn.addEventListener('click', () => {
      mobileMenu.classList.toggle('hidden');
    });

    // 3. LIGHT / DARK THEME TOGGLE LOGIC
    const themeToggle = document.getElementById('theme-toggle');
    const themeIcon = document.getElementById('theme-icon');
    const htmlEl = document.documentElement;

    themeToggle.addEventListener('click', () => {
      if (htmlEl.classList.contains('dark')) {
        htmlEl.classList.remove('dark');
        themeIcon.className = 'fas fa-sun text-amber-400 text-lg';
      } else {
        htmlEl.classList.add('dark');
        themeIcon.className = 'fas fa-moon text-brand-pink text-lg';
      }
    });

    // 4. THREE.JS LIVE PARTICLES BACKGROUND
    window.onload = function () {
      const canvas = document.getElementById('bg-canvas');
      const scene = new THREE.Scene();
      const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
      const renderer = new THREE.WebGLRenderer({ canvas: canvas, alpha: true, antialias: true });

      renderer.setSize(window.innerWidth, window.innerHeight);
      renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

      // Create ambient particle nodes
      const particleCount = 120;
      const geometry = new THREE.BufferGeometry();
      const positions = new Float32Array(particleCount * 3);
      const velocities = [];

      for (let i = 0; i < particleCount * 3; i += 3) {
        positions[i] = (Math.random() - 0.5) * 15;
        positions[i + 1] = (Math.random() - 0.5) * 15;
        positions[i + 2] = (Math.random() - 0.5) * 15;

        velocities.push({
          x: (Math.random() - 0.5) * 0.005,
          y: (Math.random() - 0.5) * 0.005,
          z: (Math.random() - 0.5) * 0.005
        });
      }

      geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));

      // Material with soft pink pink glow color
      const material = new THREE.PointsMaterial({
        color: 0xEF93C4,
        size: 0.06,
        transparent: true,
        opacity: 0.7
      });

      const particleSystem = new THREE.Points(geometry, material);
      scene.add(particleSystem);

      camera.position.z = 5;

      // Mouse interactive parallax movement
      let mouseX = 0;
      let mouseY = 0;

      window.addEventListener('mousemove', (e) => {
        mouseX = (e.clientX / window.innerWidth - 0.5) * 0.5;
        mouseY = (e.clientY / window.innerHeight - 0.5) * 0.5;
      });

      // Window resize adaptation
      window.addEventListener('resize', () => {
        camera.aspect = window.innerWidth / window.innerHeight;
        camera.updateProjectionMatrix();
        renderer.setSize(window.innerWidth, window.innerHeight);
      });

      // Animation Loop
      function animate() {
        requestAnimationFrame(animate);

        const posAttr = particleSystem.geometry.attributes.position;
        for (let i = 0; i < particleCount; i++) {
          let px = posAttr.getX(i) + velocities[i].x;
          let py = posAttr.getY(i) + velocities[i].y;
          let pz = posAttr.getZ(i) + velocities[i].z;

          // Boundary bouncing logic
          if (px > 8 || px < -8) velocities[i].x *= -1;
          if (py > 8 || py < -8) velocities[i].y *= -1;
          if (pz > 8 || pz < -8) velocities[i].z *= -1;

          posAttr.setXYZ(i, px, py, pz);
        }
        posAttr.needsUpdate = true;

        // Smooth camera dampening on cursor
        camera.position.x += (mouseX - camera.position.x) * 0.05;
        camera.position.y += (-mouseY - camera.position.y) * 0.05;
        camera.lookAt(scene.position);

        particleSystem.rotation.y += 0.001;

        renderer.render(scene, camera);
      }

      animate();
    };
  </script>
</body>
</html>
