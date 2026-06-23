<script lang="ts">
  import { onMount } from 'svelte';
  import { fade } from 'svelte/transition';
  import './app.css'
  import Home from './lib/Home.svelte';
  import Values from './lib/Values.svelte';
  import Navbar from './lib/components/Navbar.svelte';
  import CustomCursor from './lib/components/CustomCursor.svelte';
  import ThemeToggle from './lib/components/ThemeToggle.svelte';
  
  let isScrolled = false;
  let currentRoute = 'home';

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
    routeChange();
  });

  function handleScroll(e: Event) {
    const target = e.target as HTMLElement;
    isScrolled = target.scrollTop > 50;
  }
</script>

<svelte:window on:click={handleNavigation} on:popstate={routeChange} />

<CustomCursor />
<ThemeToggle />

<main class="scroll-container" on:scroll={handleScroll}>
  <Navbar {currentRoute} {isScrolled} />

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
  .scroll-container {
    height: 100vh;
    overflow-y: auto;
    scroll-snap-type: y mandatory;
    scroll-behavior: smooth;
  }
</style>
