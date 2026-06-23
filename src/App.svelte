<script lang="ts">
  import { onMount } from 'svelte';
  import { fade } from 'svelte/transition';
  import './app.css'
  import Home from './lib/Home.svelte';
  import Values from './lib/Values.svelte';
  
  let theme = 'system';
  let isScrolled = false;
  let currentRoute = 'home';
  let isForceArrow = false;

  // Mouse Tracking Glow
  let mouseX = window.innerWidth / 2;
  let mouseY = window.innerHeight / 2;

  function handleMouseMove(e: MouseEvent) {
    mouseX = e.clientX;
    mouseY = e.clientY;
  }

  function routeChange() {
    const path = window.location.pathname;
    if (path === '/our-values') {
      currentRoute = 'values';
    } else {
      currentRoute = 'home';
    }
  }

  function handleNavigation(e: MouseEvent) {
    const a = (e.target as HTMLElement).closest('a');
    if (a && a.href && a.href.startsWith(window.location.origin)) {
      const url = new URL(a.href);
      if (url.pathname === '/' || url.pathname === '/our-values') {
        if (url.hash) return; // Let anchor jumps handle themselves
        e.preventDefault();
        window.history.pushState({}, '', url.pathname);
        routeChange();
        // Reset scroll
        const scrollContainer = document.querySelector('.scroll-container');
        if (scrollContainer) scrollContainer.scrollTop = 0;
      }
    }
  }

  onMount(() => {
    // Routing
    routeChange();
    
    // 5 second hover logic to restore arrow cursor
    let hoverTimer: number;
    const handleMouseOver = (e: MouseEvent) => {
      const clickable = (e.target as HTMLElement).closest('a, button, .carousel-item, .close-btn, .floating-theme-toggle');
      if (clickable) {
        clearTimeout(hoverTimer);
        hoverTimer = window.setTimeout(() => {
          isForceArrow = true;
          document.body.classList.add('force-arrow');
        }, 600);
      }
    };

    const handleMouseOut = (e: MouseEvent) => {
      const clickable = (e.target as HTMLElement).closest('a, button, .carousel-item, .close-btn, .floating-theme-toggle');
      if (clickable) {
        clearTimeout(hoverTimer);
        isForceArrow = false;
        document.body.classList.remove('force-arrow');
      }
    };

    document.addEventListener('mouseover', handleMouseOver);
    document.addEventListener('mouseout', handleMouseOut);

    // Theme setup
    const savedTheme = localStorage.getItem('lavand-theme');
    if (savedTheme) {
      theme = savedTheme;
      applyTheme(theme);
    } else {
      applyTheme('system');
    }

    window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', e => {
      if (theme === 'system') applyTheme('system');
    });
    
    return () => {
      document.removeEventListener('mouseover', handleMouseOver);
      document.removeEventListener('mouseout', handleMouseOut);
    };
  });

  function handleScroll(e: Event) {
    const target = e.target as HTMLElement;
    isScrolled = target.scrollTop > 50;
  }

  function applyTheme(newTheme: string) {
    if (newTheme === 'system') {
      const isDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
      document.documentElement.setAttribute('data-theme', isDark ? 'dark' : 'light');
    } else {
      document.documentElement.setAttribute('data-theme', newTheme);
    }
  }

  function toggleTheme() {
    const nextTheme = (theme === 'system' || theme === 'light') ? 'dark' : 'light';
    
    // Use View Transitions API for a cinematic crossfade if supported
    // @ts-ignore
    if (document.startViewTransition) {
      // @ts-ignore
      document.startViewTransition(() => {
        theme = nextTheme;
        localStorage.setItem('lavand-theme', theme);
        applyTheme(theme);
      });
    } else {
      theme = nextTheme;
      localStorage.setItem('lavand-theme', theme);
      applyTheme(theme);
    }
  }

  function getWhatsAppUrl(text: string) {
    const message = encodeURIComponent(`Hello, I'm interested in ${text} from Lavand Royale.`);
    return `https://wa.me/?text=${message}`;
  }
</script>

<svelte:window on:mousemove={handleMouseMove} on:click={handleNavigation} on:popstate={routeChange} />

<!-- Subtle dynamic mouse glow effect -->
<div class="mouse-glow" style="--x: {mouseX}px; --y: {mouseY}px;"></div>

<!-- Custom DOM Cursor -->
<div class="custom-cursor {isForceArrow ? 'force-arrow' : ''}" style="left: {mouseX}px; top: {mouseY}px;">
  <div class="cursor-flower">
    <svg xmlns='http://www.w3.org/2000/svg' width='28' height='28' viewBox='0 0 24 24'><text y='20' font-size='20'>🪻</text></svg>
  </div>
  <div class="cursor-arrow">
    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="white" stroke="#6a4c93" stroke-width="1.5">
      <path d="M4 2L10.6 22L13.8 14.8L21 11.6L4 2Z" />
    </svg>
  </div>
</div>

<!-- Floating Theme Toggle at top right -->
<button class="floating-theme-toggle glass-panel" on:click={toggleTheme} aria-label="Toggle Theme">
  {#if document?.documentElement?.getAttribute('data-theme') === 'dark' || theme === 'dark'}
    ☀️
  {:else}
    🌙
  {/if}
</button>

<main class="scroll-container" on:scroll={handleScroll}>
  <nav class="glass-panel" class:scrolled={isScrolled}>
    <div class="links">
      {#if currentRoute === 'home'}
        <a href="/#carousel-section">Aromas</a>
      {:else}
        <a href="/">Home</a>
      {/if}
    </div>
    <div class="logo">Lavand Royale</div>
    <div class="nav-actions">
      <a href={getWhatsAppUrl('your collections')} target="_blank" class="btn-primary" style="padding: 0.5rem 1.5rem; display: flex; align-items: center; gap: 0.5rem;">
        <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect><path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path><line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line></svg>
        Order
      </a>
    </div>
  </nav>

  {#if currentRoute === 'home'}
    <div in:fade={{ duration: 800, delay: 200 }}>
      <Home />
    </div>
  {:else}
    <div in:fade={{ duration: 800, delay: 200 }}>
      <Values />
    </div>
  {/if}
</main>

<style>
  /* Custom DOM Cursor */
  .custom-cursor {
    position: fixed;
    pointer-events: none;
    z-index: 10000;
    transform: translate(-4px, -4px); /* Align the SVG tip */
  }

  .cursor-flower, .cursor-arrow {
    position: absolute;
    top: 0; left: 0;
    transition: opacity 0.3s ease, transform 0.3s ease;
  }

  .cursor-flower {
    opacity: 1;
    transform: scale(1);
  }

  .cursor-arrow {
    opacity: 0;
    transform: scale(0.5);
  }

  .custom-cursor.force-arrow .cursor-flower {
    opacity: 0;
    transform: scale(1.5);
  }

  .custom-cursor.force-arrow .cursor-arrow {
    opacity: 1;
    transform: scale(1);
  }
  /* Mouse Glow Tracker */
  .mouse-glow {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    pointer-events: none;
    z-index: 9999;
    background: radial-gradient(
      600px circle at var(--x) var(--y), 
      rgba(255, 255, 255, 0.04),
      transparent 40%
    );
  }

  :root[data-theme="dark"] .mouse-glow {
    background: radial-gradient(
      600px circle at var(--x) var(--y), 
      rgba(255, 255, 255, 0.08),
      transparent 40%
    );
  }

  .scroll-container {
    height: 100vh;
    overflow-y: auto;
    scroll-snap-type: y mandatory;
    scroll-behavior: smooth;
  }

  nav {
    position: fixed;
    top: 1.5rem;
    left: 50%;
    transform: translateX(-50%);
    width: 90%;
    max-width: 1200px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 2rem;
    z-index: 1000;
    border-radius: 50px;
    transition: all 0.5s cubic-bezier(0.25, 0.8, 0.25, 1);
  }

  nav.scrolled {
    top: 0;
    width: 100%;
    max-width: 100%;
    border-radius: 0;
    padding: 1rem 5%;
    background: rgba(255, 255, 255, 0.15);
    backdrop-filter: blur(40px);
    -webkit-backdrop-filter: blur(40px);
    border: none;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
    box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
  }
  
  :root[data-theme="dark"] nav.scrolled {
    background: rgba(18, 18, 18, 0.3);
    border-bottom: 1px solid rgba(255, 255, 255, 0.05);
  }

  .links {
    display: flex;
    gap: 2rem;
    flex: 1;
    transition: opacity 0.3s ease, transform 0.3s ease;
  }

  nav.scrolled .links {
    opacity: 0;
    pointer-events: none;
    transform: translateY(-10px);
  }

  .links a {
    font-weight: 600;
    font-size: 0.95rem;
  }

  .logo {
    font-size: 1.8rem;
    font-weight: 700;
    color: var(--color-lavender);
    letter-spacing: 2px;
    text-transform: uppercase;
    text-align: center;
    flex: 1;
    transition: font-size 0.3s;
  }
  
  nav.scrolled .logo {
    font-size: 1.5rem;
  }

  .nav-actions {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    gap: 1.5rem;
    flex: 1;
  }

  .floating-theme-toggle {
    position: fixed;
    top: calc(1.5rem + 130px);
    right: 1.5rem;
    width: 45px;
    height: 45px;
    border-radius: 50%;
    font-size: 1.3rem;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1500;
  }
  
  .floating-theme-toggle:hover {
    transform: scale(1.1);
    box-shadow: 0 4px 10px rgba(181, 126, 220, 0.4);
  }

  @media (max-width: 768px) {
    nav {
      flex-direction: column;
      gap: 1rem;
      border-radius: 20px;
    }
    
    nav.scrolled {
      flex-direction: row;
      gap: 0;
    }

    .links, .nav-actions {
      justify-content: center;
      width: 100%;
    }
    
    nav.scrolled .links {
      display: none;
    }
  }
</style>
