<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <!-- Responsive viewport -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Lasbon Rodrigues - Portfolio</title>
  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
  <!-- Swiper CSS for slider -->
  <link rel="stylesheet" href="https://unpkg.com/swiper@8.4.7/swiper-bundle.min.css" />
  <!-- Font Awesome Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" />
  <style>
    /* ==============================
       CSS Variables & Bee Inspired Colors
    ============================== */
    :root {
      --primary-color: #FFD700; /* Bee Yellow */
      --secondary-color: #1E90FF;
      --accent-color: #F0E68C;
      --header-footer-bg: #0a163b; /* Initial header background */
      --header-text: #fff;
      --toggle-text: #fff;
      --content-text: #fff;
      --text-dark: #333;
      --text-light: #fff;
      --heading-color: var(--text-dark);
      --glass-bg: rgba(255, 255, 255, 0.85);
      --body-bg: #fff;
      --footer-bg: #333;
    }
    /* Dark mode variables */
    body.dark-mode {
      --body-bg: #121212;
      --text-dark: #fff;
      --text-light: #fff;
      --secondary-color: #939600;
      background: var(--body-bg);
      color: var(--text-dark);
      /* Define a dark hover background variable for better contrast */
      --dark-hover-bg: #555;
    }
    body.dark-mode header { background: #1f1f1f; }
    body.dark-mode .nav-links a { color: var(--header-text); }
    body.dark-mode .nav-links a:hover { color: var(--accent-color); }
    body.dark-mode .glass {
      background: rgba(30,30,30,0.85);
      border: 1px solid rgba(255,255,255,0.2);
      box-shadow: 0 0 20px rgba(0,0,0,0.8), 0 4px 6px rgba(0,0,0,0.1);
    }
    body.dark-mode footer { background: var(--footer-bg); }
    /* Dark mode override for certification texts */
    body.dark-mode .certification,
    body.dark-mode .certification h3,
    body.dark-mode .certification ul,
    body.dark-mode .certification ul li {
      color: #000 !important;
    }
    
    /* ==============================
       Moving Pattern Background
    ============================== */
    .pattern {
      position: fixed;
      top: 0; left: 0;
      width: 100%;
      height: 100%;
      z-index: -2;
      background-image: repeating-linear-gradient(45deg, rgba(0, 0, 0, 0.03) 0, rgba(0, 0, 0, 0.03) 1px, transparent 1px, transparent 20px);
      background-size: 40px 40px;
      pointer-events: none;
    }
    
    /* ==============================
       Global Reset & Base Styles
    ============================== */
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: 'Roboto', sans-serif;
      background: var(--body-bg);
      color: var(--text-dark);
      line-height: 1.6;
      scroll-behavior: smooth;
      padding-top: 80px;
    }
    @media (max-width: 1024px) { body { padding-top: 120px; } }
    @media (max-width: 480px) { body { padding-top: 140px; } }
    
    /* ==============================
       Preloader with Zoom-In Effect
    ============================== */
    #preloader {
      position: fixed; top: 0; left: 0; width: 100%; height: 100%;
      background-color: #000;
      display: flex; align-items: center; justify-content: center;
      z-index: 2000; transition: opacity 0.5s ease;
    }
    #preloader .loader-text {
      font-size: 3rem;
      color: var(--text-light);
      letter-spacing: 8px;
      animation: zoomIn 1.5s ease-out forwards;
    }
    @keyframes zoomIn {
      0% { transform: scale(0); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }
    
    /* ==============================
       Intersection Observer Animation
    ============================== */
    .animate { opacity: 0; transform: translateY(20px); }
    .animate.visible { opacity: 1; transform: translateY(0); transition: all 0.8s ease-out; }
    
    /* ==============================
       Glassmorphism Effect & Hover Color Change
    ============================== */
    .glass {
      background: var(--glass-bg);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border: 1px solid rgba(255,255,255,0.5);
      border-radius: 15px;
      padding: 20px;
      box-shadow: 0 0 20px rgba(255,255,255,0.6), 0 4px 6px rgba(0,0,0,0.1);
      transition: background 0.3s ease, box-shadow 0.3s ease, transform 0.3s ease;
    }
    .glass:hover {
      background: rgba(240,230,140,0.9);
      box-shadow: 0 0 30px rgba(255,255,255,0.8), 0 4px 6px rgba(0,0,0,0.1);
      transform: translateY(-3px);
    }
    /* In dark mode, on hover change the box background to a dark hover color for better contrast */
    body.dark-mode .glass:hover {
      background: var(--dark-hover-bg);
    }
    
    /* ==============================
       Header & Navigation
    ============================== */
    header {
      position: fixed;
      top: 0; left: 0; width: 100%;
      background: var(--header-footer-bg);
      color: var(--header-text);
      padding: 0.5rem 2%;
      z-index: 1000;
      box-shadow: 0 2px 5px rgba(0,0,0,0.15);
    }
    .navbar {
      max-width: 1200px;
      margin: 0 auto;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
    }
    .logo a {
      color: var(--header-text);
      font-size: 1.8rem;
      font-weight: 700;
      text-decoration: none;
    }
    .nav-links {
      list-style: none;
      display: flex;
      flex-wrap: wrap;
    }
    .nav-links li { margin: 0 10px; }
    .nav-links a {
      position: relative;
      text-decoration: none;
      color: var(--header-text);
      font-size: 1rem;
      transition: color 0.3s ease;
    }
    .nav-links a::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: -3px;
      width: 0;
      height: 3px;
      background: var(--secondary-color);
      transition: width 0.3s ease;
    }
    .nav-links a:hover::after { width: 100%; }
    .nav-links a:hover { color: var(--accent-color); }
    /* Active nav link styling */
    .nav-links a.active {
      color: var(--accent-color);
      font-weight: bold;
    }
    #dark-mode-toggle {
      background: var(--primary-color);
      border: none;
      padding: 0.5rem 1rem;
      border-radius: 5px;
      cursor: pointer;
      color: var(--toggle-text);
      transition: background 0.3s ease;
      margin: 10px 0;
    }
    #dark-mode-toggle:hover { background: var(--accent-color); }
    #theme-toggle-container {
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
      margin: 10px 0;
      transition: opacity 0.3s ease;
    }
    .theme-btn {
      background: var(--primary-color);
      border: none;
      padding: 0.5rem 1rem;
      border-radius: 5px;
      cursor: pointer;
      color: var(--content-text);
      transition: background 0.3s ease;
    }
    .theme-btn:hover { background: var(--accent-color); }
    @media (max-width: 1024px) {
      .navbar { flex-direction: column; align-items: center; }
      .logo a { font-size: 1.5rem; margin-bottom: 10px; text-align: center; }
      .nav-links { justify-content: center; margin-top: 5px; }
      #dark-mode-toggle, #theme-toggle-container { margin-top: 10px; }
    }
    @media (max-width: 480px) {
      .logo a { font-size: 1.3rem; }
      .nav-links a { font-size: 0.9rem; }
    }
    
    /* ==============================
       Section Base & Containers
    ============================== */
    section { padding: 4rem 2%; transition: opacity 0.5s ease; }
    .section-container { max-width: 1200px; margin: 0 auto; }
    
    /* ==============================
       HERO SECTION (Home)
    ============================== */
    .hero {
      background: var(--secondary-color);
      min-height: 90vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 6rem 2% 2rem;
      position: relative;
    }
    /* Added margin-top so the hero container is not hidden behind the fixed header */
    .hero-container {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      justify-content: center;
      width: 100%;
      max-width: 1200px;
      margin-top: 100px;
    }
    .hero-content {
      flex: 1 1 400px;
      text-align: center;
    }
    .hero-content h1 {
      font-size: 3rem;
      margin-bottom: 10px;
      color: var(--heading-color);
    }
    /* Updated header title */
    .hero-content h2 {
      font-size: 1.5rem;
      margin-bottom: 10px;
      color: var(--heading-color);
    }
    /* Updated tagline text */
    .hero-content p {
      font-size: 1rem;
      margin-bottom: 20px;
      max-width: 600px;
      color: var(--text-dark);
    }
    .cta-buttons {
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
      justify-content: center;
    }
    .cta-buttons a {
      flex: 1 1 150px;
      text-align: center;
      padding: 0.75rem 1.5rem;
      border-radius: 5px;
      text-decoration: none;
      color: var(--content-text);
      background: var(--primary-color);
      transition: background 0.3s ease;
    }
    .cta-buttons a:hover { background: var(--accent-color); }
    .hero-image {
      flex: 1 1 400px;
      text-align: center;
      position: relative;
    }
    .hero-image img {
      width: 100%;
      max-width: 400px;
      border-radius: 50%;
      object-fit: cover;
      box-shadow: 0 10px 30px rgba(0,0,0,0.1);
      position: relative;
      z-index: 2;
    }
    /* Hide hero image on screens with width 893px or less */
    @media (max-width: 893px) {
      .hero-image { display: none; }
    }
    @media (max-width: 1024px) {
      .hero {
        flex-direction: column;
        text-align: center;
        min-height: auto;
        padding: 6rem 1rem 2rem;
        padding-top: 200px !important;
      }
      .hero-image img { max-width: 280px; margin: 0 auto; }
      .nav-links { justify-content: center; }
    }
    @media (max-width: 480px) {
      .hero { padding-top: 220px !important; }
      .hero-content h1 { font-size: 2rem; }
      .hero-content h2 { font-size: 1.2rem; }
      .hero-content p { font-size: 0.9rem; }
      .cta-buttons a { flex: 1 1 130px; padding: 0.5rem 1rem; text-align: center; }
      .navbar { padding: 0.5rem 1rem; }
      .nav-links li { margin: 0.3rem; }
    }
    @media (max-width: 320px) {
      .hero { padding-top: 250px !important; }
      .hero-content h1 { font-size: 1.5rem; }
      .hero-content h2 { font-size: 1rem; }
      .hero-content p { font-size: 0.8rem; }
      .cta-buttons a { flex: 1 1 110px; padding: 0.4rem 0.8rem; }
    }
    
    /* ==============================
       ABOUT SECTION
    ============================== */
    .about-container { text-align: center; }
    .about-container h2 {
      font-size: 2rem;
      margin-bottom: 20px;
      color: var(--heading-color);
    }
    .about-container p {
      font-size: 1rem;
      text-align: center;
      max-width: 800px;
      margin: 0 auto 20px;
      color: var(--text-dark);
    }
    
    /* ==============================
       SKILLS SECTION (Slider with Dropdowns)
    ============================== */
    .skills-container h2 {
      font-size: 2rem;
      margin-bottom: 20px;
      color: var(--heading-color);
      text-align: center;
    }
    .skill-card { padding: 20px; }
    details { cursor: pointer; }
    details summary { font-size: 1.5rem; font-weight: bold; }
    details p { margin-top: 10px; font-size: 1rem; }
    
    /* Swiper Overrides */
    .swiper { padding: 20px 0; }
    .swiper-slide { display: flex; justify-content: center; }
    /* Responsive Breakpoints for Swiper */
    @media (max-width: 640px) {
      .mySwiper { width: 100%; }
      .swiper-slide { width: auto; }
    }
    
    /* ==============================
       PROJECTS SECTION
    ============================== */
    .projects-container { text-align: center; }
    .projects-container h1 {
      font-size: 2rem;
      margin-bottom: 20px;
      color: var(--heading-color);
    }
    .projects {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      justify-content: center;
    }
    .project {
      background: #fff;
      border-radius: 8px;
      padding: 20px;
      width: 300px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.2);
      transition: transform 0.3s ease;
    }
    .project:hover { transform: translateY(-5px); }
    .project h3 { margin-top: 10px; font-size: 1.2rem; }
    .project ul { list-style: disc; padding-left: 20px; margin-top: 10px; }
    .project ul li { font-size: 0.9rem; }
    /* Using Font Awesome icons for projects */
    .project .icon {
      font-size: 4rem;
      color: var(--primary-color);
      margin-bottom: 10px;
    }
    
    /* Dark mode override for project texts (make them black) */
    body.dark-mode .projects-container .project,
    body.dark-mode .projects-container .project h3,
    body.dark-mode .projects-container .project ul,
    body.dark-mode .projects-container .project ul li {
      color: #000 !important;
    }
    
    /* ==============================
       CERTIFICATION SECTION (Side Format)
    ============================== */
    .certification-container {
      text-align: center;
    }
    .certification-container h1 {
      font-size: 2rem;
      margin-bottom: 20px;
      color: var(--heading-color);
    }
    .certifications {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      justify-content: center;
    }
    .certification {
      background: #fff;
      border-radius: 8px;
      padding: 20px;
      flex: 1 1 300px;
      max-width: 350px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.2);
      text-align: left;
    }
    .certification h3 {
      font-size: 1rem;
      margin-bottom: 10px;
    }
    .certification ul {
      list-style: disc;
      padding-left: 20px;
    }
    .certification ul li {
      font-size: 0.9rem;
      margin-bottom: 5px;
    }
    .cert-image {
      margin-top: 10px;
      text-align: center;
    }
    /* Certification icons styling */
    .cert-icon {
      font-size: 3rem;
      color: var(--primary-color);
      text-align: center;
      margin-bottom: 10px;
    }
    /* For Linux and ITIL 4, add links on the certificate text */
    .cert-link {
      text-align: center;
      font-style: italic;
      margin-top: 5px;
    }
    .cert-link a {
      color: var(--primary-color);
      text-decoration: none;
    }
    
    /* ==============================
       CONTACT SECTION
    ============================== */
    .contact-container { text-align: center; }
    .contact-container h2 {
      font-size: 2rem;
      margin-bottom: 20px;
      color: var(--heading-color);
    }
    .contact-container form {
      max-width: 600px;
      margin: 0 auto;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
    .contact-container form input,
    .contact-container form textarea {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-size: 1rem;
    }
    .contact-container form button {
      padding: 10px 20px;
      background: #333;
      color: #fff;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      transition: background 0.3s ease;
    }
    .contact-container form button:hover { background: #555; }
    
    /* ==============================
       Footer
    ============================== */
    footer {
      background: var(--footer-bg);
      color: var(--text-light);
      text-align: center;
      padding: 20px;
      box-shadow: 0 0 20px rgba(0,0,0,0.5);
    }
    footer p { margin-top: 10px; font-size: 1rem; }
    .social-links {
      display: flex;
      justify-content: center;
      gap: 20px;
      margin: 20px 0;
    }
    .social-links a {
      color: var(--text-light);
      font-size: 1.5rem;
      transition: transform 0.3s ease;
    }
    .social-links a:hover { transform: translateY(-3px); }
    
    @media (max-width: 1024px) {
      .hero { flex-direction: column; text-align: center; min-height: auto; padding: 6rem 1rem 2rem; padding-top: 200px !important; }
      .hero-image img { max-width: 280px; margin: 0 auto; }
      .nav-links { justify-content: center; }
    }
    @media (max-width: 480px) {
      .hero { padding-top: 220px !important; }
      .hero-content h1 { font-size: 2rem; }
      .hero-content h2 { font-size: 1.2rem; }
      .hero-content p { font-size: 0.9rem; }
      .cta-buttons a { flex: 1 1 130px; padding: 0.5rem 1rem; text-align: center; }
      .navbar { padding: 0.5rem 1rem; }
      .nav-links li { margin: 0.3rem; }
    }
    @media (max-width: 320px) {
      .hero { padding-top: 250px !important; }
      .hero-content h1 { font-size: 1.5rem; }
      .hero-content h2 { font-size: 1rem; }
      .hero-content p { font-size: 0.8rem; }
      .cta-buttons a { flex: 1 1 110px; padding: 0.4rem 0.8rem; }
    }
  </style>
</head>
<body>
  <!-- Moving Pattern Background -->
  <div class="pattern"></div>
  
  <!-- Preloader -->
  <div id="preloader">
    <div class="loader-text">LASBON</div>
  </div>
  
  <!-- HEADER & NAVIGATION -->
  <header>
    <nav class="navbar">
      <div class="logo">
        <a href="#hero">Lasbon Rodrigues</a>
      </div>
      <ul class="nav-links">
        <li><a href="#hero">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#skills">Skills</a></li>
        <li><a href="#projects">Projects</a></li>
        <li><a href="#certification">Certification</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
      <!-- Dark Mode Toggle Button -->
      <button id="dark-mode-toggle">Dark Mode</button>
      <!-- Theme Option Toggle Buttons (Vertical) -->
      <div id="theme-toggle-container">
        <button class="theme-btn" data-theme="original">Original</button>
        <button class="theme-btn" data-theme="greenWhite">Green &amp; White</button>
        <button class="theme-btn" data-theme="red">Red</button>
        <button class="theme-btn" data-theme="purple">Purple</button>
      </div>
    </nav>
  </header>
  
  <main>
    <!-- HERO SECTION -->
    <section class="hero animate highlighted visible" id="hero" style="padding-top: 100px; padding-bottom: 64px;">
      <div class="section-container hero-container glass animate visible">
        <div class="hero-content animate visible">
          <h1>Lasbon Rodrigues</h1>
          <!-- Updated header title -->
          <h2 id="typewriter-title">IT Support Engineer</h2>
          <!-- Updated tagline text -->
          <p id="typewriter-text">
            Ensuring seamless IT operations through expert technical support, system administration, and network management.
          </p>
          <div class="cta-buttons">
            <a href="#contact" class="pulse">Get in Touch</a>
            <!-- Download CV opens in a new page -->
            <a href="lasbonrodrigues.pdf" target="_blank">Download CV</a>
          </div>
        </div>
        <div class="hero-image animate visible">
          <img src="lasbonr.jpg" alt="Lasbon Rodrigues">
        </div>
      </div>
    </section>
    
    <!-- ABOUT SECTION -->
    <section id="about" class="section">
      <div class="section-container about-container glass animate">
        <h2>About Me</h2>
        <p>I am a passionate IT Support Engineer with experience troubleshooting technical issues, managing IT infrastructure, and supporting end users across various systems and networks.</p>
      </div>
    </section>
    
    <!-- SKILLS SECTION (Slider with Dropdowns) -->
    <section id="skills" class="section">
      <div class="section-container skills-container glass animate">
        <h2>Skills</h2>
        <!-- Swiper Container -->
        <div class="swiper mySwiper">
          <div class="swiper-wrapper">
            <!-- Slide for SQL -->
            <div class="swiper-slide">
              <div class="skill-card glass">
                <details>
                  <summary>SQL</summary>
                  <p>Proficient in writing queries and managing relational databases such as MySQL and PostgreSQL.</p>
                </details>
              </div>
            </div>
            <!-- Slide for MS Excel -->
            <div class="swiper-slide">
              <div class="skill-card glass">
                <details>
                  <summary>MS Excel</summary>
                  <p>Skilled in data analysis, pivot tables, and advanced formulas for effective data management.</p>
                </details>
              </div>
            </div>
            <!-- Slide for MS Office -->
            <div class="swiper-slide">
              <div class="skill-card glass">
                <details>
                  <summary>MS Office</summary>
                  <p>Expert in Word, PowerPoint, and Outlook for efficient document creation and business communication.</p>
                </details>
              </div>
            </div>
            <!-- Slide for Networking -->
            <div class="swiper-slide">
              <div class="skill-card glass">
                <details>
                  <summary>Networking</summary>
                  <p>Experienced in configuring and troubleshooting network infrastructures and protocols.</p>
                </details>
              </div>
            </div>
            <!-- Slide for Cisco Packet Tracer / CCNA -->
            <div class="swiper-slide">
              <div class="skill-card glass">
                <details>
                  <summary>Cisco Packet Tracer / CCNA</summary>
                  <p>Familiar with Cisco simulation tools and equipped with CCNA-level understanding of network fundamentals.</p>
                </details>
              </div>
            </div>
            <!-- New Slide for Linux -->
            <div class="swiper-slide">
              <div class="skill-card glass">
                <details>
                  <summary>Linux</summary>
                  <p>Experienced in UNIX/Linux system administration and troubleshooting, ensuring efficient IT operations.</p>
                </details>
              </div>
            </div>
          </div>
          <!-- Side Navigation Buttons -->
          <div class="swiper-button-next"></div>
          <div class="swiper-button-prev"></div>
        </div>
      </div>
    </section>
    
    <!-- PROJECTS SECTION -->
    <section id="projects" class="section">
      <div class="section-container projects-container glass animate">
        <h1>My Projects</h1>
        <div class="projects">
          <!-- IOT Based Smart Mirror Project -->
          <div class="project animate">
            <i class="fas fa-globe icon"></i>
            <h3>IOT Based Smart Mirror | 2020</h3>
            <ul>
              <li>Designed and developed an IoT-based smart mirror solution using Python and various hardware components.</li>
              <li>The IOT Smart Mirror displayed time, weather updates and news feeds.</li>
              <li>IOT Based Smart Mirror (IRJET) – <a href="https://www.irjet.net/archives/V8/i3/IRJET-V8I3567.pdf" target="_blank">IRJET Link</a></li>
            </ul>
          </div>
          <!-- ZIGBEE Based Humidity and Temperature Monitoring Sensor Project -->
          <div class="project animate">
            <i class="fas fa-thermometer-half icon"></i>
            <h3>ZIGBEE Based Humidity and Temperature Monitoring Sensor | 2016</h3>
            <ul>
              <li>Designed a monitoring system using Zigbee technology to measure and display environmental data.</li>
            </ul>
          </div>
        </div>
      </div>
    </section>
    
    <!-- CERTIFICATION SECTION (Side Format) -->
    <section id="certification" class="section">
      <div class="section-container certification-container glass animate">
        <h1>Certifications</h1>
        <div class="certifications">
          <!-- CCNA Certification with clickable verification number -->
          <div class="certification animate">
            <div class="cert-icon">
              <i class="fas fa-network-wired"></i>
            </div>
            <h3>CCNA (Cisco Certified Network Associate) – Verification Number: <a href="https://drive.google.com/file/d/1mrHovdsa2Ecy4hrnDVugYe5fOThDmhzh/view?usp=sharing" target="_blank">[3e68dfead361479dae8b93ce127213e5]</a></h3>
            <ul>
              <li>Completed CCNA certification covering networking fundamentals, routing and switching, network security, and troubleshooting techniques.</li>
            </ul>
          </div>
          <!-- Linux Certification -->
          <div class="certification animate">
            <div class="cert-icon">
              <i class="fab fa-linux"></i>
            </div>
            <h3>LINUX</h3>
            <ul>
              <li>Learned fundamentals of Linux on Education Platform Udemy.</li>
            </ul>
            <div class="cert-link">
              <a href="https://udemy-certificate.s3.amazonaws.com/image/UC-440bcf45-955e-4503-98d2-0962ad5a66d6.jpg" target="_blank">Linux Certificate</a>
            </div>
          </div>
          <!-- ITIL 4 Certification -->
          <div class="certification animate">
            <div class="cert-icon">
              <i class="fas fa-certificate"></i>
            </div>
            <h3>ITIL 4</h3>
            <ul>
              <li>Learned fundamentals of ITIL 4 on Education Platform Udemy.</li>
            </ul>
            <div class="cert-link">
              <a href="https://udemy-certificate.s3.amazonaws.com/image/UC-d9e7bb5f-605e-4ad0-8f30-46e6a779d6ce.jpg" target="_blank">ITIL 4 Certificate</a>
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- CONTACT SECTION -->
    <section id="contact" class="section contact">
      <div class="section-container contact-container glass animate">
        <h2>Contact Me</h2>
        <form>
          <input type="text" placeholder="Your Name" required>
          <input type="email" placeholder="Your Email" required>
          <textarea placeholder="Your Message" required></textarea>
          <button type="submit">Send Message</button>
        </form>
      </div>
    </section>
  </main>
  
  <!-- FOOTER -->
  <footer>
    <div class="social-links">
      <a href="https://www.linkedin.com/in/lasbon-rodrigues-946547bb/" target="_blank"><i class="fab fa-linkedin"></i></a>
      <a href="https://github.com/lasbon" target="_blank"><i class="fab fa-github"></i></a>
      <a href="mailto:rlasbon@gmail.com"><i class="fas fa-envelope"></i></a>
      <a href="https://wa.me/919819440672" target="_blank"><i class="fab fa-whatsapp"></i></a>
    </div>
    <p>&copy; 2023 Lasbon Rodrigues. All rights reserved.</p>
  </footer>
  
  <!-- Swiper JS -->
  <script src="https://unpkg.com/swiper@8.4.7/swiper-bundle.min.js"></script>
  
  <!-- Other Scripts -->
  <script>
    // Preloader: Hide after page loads
    window.onload = function() {
      setTimeout(function() {
        var preloader = document.getElementById("preloader");
        preloader.style.opacity = 0;
        setTimeout(function() { preloader.style.display = "none"; }, 500);
      }, 1000);
    };

    // Intersection Observer for Fade-In Effect on Scroll
    document.addEventListener("DOMContentLoaded", function() {
      let observer = new IntersectionObserver((entries, observer) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add("visible");
            observer.unobserve(entry.target);
          }
        });
      }, { threshold: 0.1 });
      document.querySelectorAll(".animate").forEach(el => { observer.observe(el); });
    });
    
    // Updated Navigation Smooth Scroll Script
    document.addEventListener('DOMContentLoaded', function() {
      const navLinks = document.querySelectorAll('.nav-links a');
      navLinks.forEach(link => {
        link.addEventListener('click', function(e) {
          e.preventDefault();
          const targetId = this.getAttribute('href').substring(1);
          const targetElement = document.getElementById(targetId);
          // For Projects and Certification, offset for fixed header
          if (targetId === "projects" || targetId === "certification") {
            const headerHeight = document.querySelector("header").offsetHeight;
            window.scrollTo({ top: targetElement.offsetTop - headerHeight, behavior: 'smooth' });
          } else {
            targetElement.scrollIntoView({ behavior: 'smooth', block: 'center' });
          }
        });
      });
    });

    // Scrollspy: Highlight active navigation link based on section in view
    document.addEventListener('DOMContentLoaded', function() {
      const sections = document.querySelectorAll('section');
      const navLinks = document.querySelectorAll('.nav-links a');

      const options = {
        threshold: 0.5
      };

      const sectionObserver = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            navLinks.forEach(link => {
              link.classList.remove('active');
              if(link.getAttribute('href').substring(1) === entry.target.id) {
                link.classList.add('active');
              }
            });
          }
        });
      }, options);

      sections.forEach(section => {
        sectionObserver.observe(section);
      });
    });
    
    // Dark Mode Toggle Script
    const darkModeToggle = document.getElementById("dark-mode-toggle");
    darkModeToggle.addEventListener("click", function() {
      document.body.classList.toggle("dark-mode");
      if (document.body.classList.contains("dark-mode")) {
        document.documentElement.style.setProperty('--heading-color', '#fff');
      } else {
        const theme = themes[currentTheme];
        document.documentElement.style.setProperty('--heading-color', theme['--heading-color']);
      }
      darkModeToggle.innerText = document.body.classList.contains("dark-mode") ? "Light Mode" : "Dark Mode";
    });
    
    // Theme Option Toggle Script
    let currentTheme = "original";
    const themes = {
      original: {
        '--primary-color': '#1E90FF',
        '--secondary-color': '#FFD700',
        '--accent-color': '#F0E68C',
        '--header-footer-bg': '#001f3f',
        '--header-text': '#fff',
        '--toggle-text': '#fff',
        '--content-text': '#fff',
        '--text-dark': '#333',
        '--body-bg': '#f0f8ff',
        '--heading-color': '#333',
        '--footer-bg': '#001f3f'
      },
      greenWhite: {
        '--primary-color': '#228B22',
        '--secondary-color': '#FFD700',
        '--accent-color': '#F0E68C',
        '--header-footer-bg': '#FFFFFF',
        '--header-text': '#228B22',
        '--toggle-text': '#fff',
        '--content-text': '#fff',
        '--text-dark': '#333',
        '--body-bg': '#FFFFFF',
        '--heading-color': '#228B22',
        '--footer-bg': '#228B22'
      },
      red: {
        '--primary-color': '#FF0000',
        '--secondary-color': '#FFFFFF',
        '--accent-color': '#F0E68C',
        '--header-footer-bg': '#8B0000',
        '--header-text': '#fff',
        '--toggle-text': '#fff',
        '--content-text': '#fff',
        '--text-dark': '#333',
        '--body-bg': '#FFFFFF',
        '--heading-color': '#FF0000',
        '--footer-bg': '#8B0000'
      },
      purple: {
        '--primary-color': '#7a1e6a',
        '--secondary-color': '#7a1e6a',
        '--accent-color': '#F0E68C',
        '--header-footer-bg': '#000',
        '--header-text': '#fff',
        '--toggle-text': '#fff',
        '--content-text': '#fff',
        '--text-dark': '#333',
        '--body-bg': '#F5F5F5',
        '--heading-color': '#7a1e6a',
        '--footer-bg': '#7a1e6a'
      }
    };
    const themeButtons = document.querySelectorAll('.theme-btn');
    themeButtons.forEach(btn => {
      btn.addEventListener('click', function() {
        const themeKey = this.getAttribute('data-theme');
        currentTheme = themeKey;
        const theme = themes[themeKey];
        for (let variable in theme) {
          document.documentElement.style.setProperty(variable, theme[variable]);
        }
      });
    });
    
    // Swiper Initialization for Skills Slider (3 slides per view) with responsive breakpoints
    var swiper = new Swiper(".mySwiper", {
      navigation: {
        nextEl: ".swiper-button-next",
        prevEl: ".swiper-button-prev",
      },
      slidesPerView: 3,
      spaceBetween: 20,
      loop: true,
      breakpoints: {
        320: { slidesPerView: 1, spaceBetween: 10 },
        640: { slidesPerView: 2, spaceBetween: 20 },
        1024: { slidesPerView: 3, spaceBetween: 20 }
      }
    });
    
    // Moving Pattern Background Animation on Scroll
    window.addEventListener('scroll', () => {
      const scrollY = window.scrollY;
      document.querySelector('.pattern').style.backgroundPositionY = scrollY * 0.5 + 'px';
      
      // For devices with viewport width ≤1014px, hide the theme toggle container when scrolled away from the top
      if(window.innerWidth <= 1014) {
        const themeContainer = document.getElementById("theme-toggle-container");
        if(scrollY > 0) {
          themeContainer.style.display = 'none';
        } else {
          themeContainer.style.display = 'flex';
        }
      }
    });
  </script>
  
</body>
</html>
