<script lang="ts">
  import { onMount } from 'svelte';
  export let theme = 'system';

  onMount(() => {
    const savedTheme = localStorage.getItem('lavand-theme');
    if (savedTheme) {
      theme = savedTheme;
      applyTheme(theme);
    } else {
      applyTheme('system');
    }

    window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', () => {
      if (theme === 'system') applyTheme('system');
    });
  });

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
</script>

<button class="floating-theme-toggle glass-panel" on:click={toggleTheme} aria-label="Toggle Theme">
  {#if document?.documentElement?.getAttribute('data-theme') === 'dark' || theme === 'dark'}
    ☀️
  {:else}
    🌙
  {/if}
</button>

<style>
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
    transition: transform 0.3s;
  }
  
  .floating-theme-toggle:hover {
    transform: scale(1.1);
  }
</style>
