<script lang="ts">
  import { onMount } from 'svelte';
  export let mouseX = typeof window !== 'undefined' ? window.innerWidth / 2 : 0;
  export let mouseY = typeof window !== 'undefined' ? window.innerHeight / 2 : 0;
  
  let isForceArrow = false;

  function handleMouseMove(e: MouseEvent) {
    mouseX = e.clientX;
    mouseY = e.clientY;
  }

  onMount(() => {
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

    return () => {
      document.removeEventListener('mouseover', handleMouseOver);
      document.removeEventListener('mouseout', handleMouseOut);
    };
  });
</script>

<svelte:window on:mousemove={handleMouseMove} />

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

<style>
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
</style>
