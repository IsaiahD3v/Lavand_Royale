<script lang="ts">
  export let currentRoute: string;
  export let isScrolled: boolean;

  let isMobileMenuOpen = false;

  const instagramUrl = "https://instagram.com/lavandroyale";
</script>

<nav class:scrolled={isScrolled}>
  <div class="links">
    {#if currentRoute === "home"}
      <a href="/#home-page">Aromas</a>
    {:else}
      <a href="/">Início</a>
    {/if}
  </div>
  <div class="logo">
    <svg
      class="vine vine-left"
      viewBox="0 0 100 24"
      width="50"
      height="15"
      fill="none"
      stroke="currentColor"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
    >
      <path d="M0 12 Q 25 2, 50 12 T 100 12" />
      <path
        d="M15 7 Q 20 0, 25 5 Q 20 10, 15 7 Z"
        fill="currentColor"
        stroke="none"
      />
      <path
        d="M45 17 Q 50 24, 55 19 Q 50 14, 45 17 Z"
        fill="currentColor"
        stroke="none"
      />
      <path
        d="M75 7 Q 80 0, 85 5 Q 80 10, 75 7 Z"
        fill="currentColor"
        stroke="none"
      />
    </svg>
    Lavande Royale
    <svg
      class="vine vine-right"
      viewBox="0 0 100 24"
      width="50"
      height="15"
      fill="none"
      stroke="currentColor"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
    >
      <path d="M0 12 Q 25 2, 50 12 T 100 12" />
      <path
        d="M15 7 Q 20 0, 25 5 Q 20 10, 15 7 Z"
        fill="currentColor"
        stroke="none"
      />
      <path
        d="M45 17 Q 50 24, 55 19 Q 50 14, 45 17 Z"
        fill="currentColor"
        stroke="none"
      />
      <path
        d="M75 7 Q 80 0, 85 5 Q 80 10, 75 7 Z"
        fill="currentColor"
        stroke="none"
      />
    </svg>
  </div>
  <div class="nav-actions">
    <a
      href={instagramUrl}
      target="_blank"
      class="btn-primary"
      style="padding: 0.5rem 1.5rem; display: flex; align-items: center; gap: 0.5rem;"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="18"
        height="18"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round"
        ><rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect><path
          d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"
        ></path><line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line></svg
      >
      Comprar
    </a>
  </div>
</nav>

{#if isMobileMenuOpen}
  <!-- svelte-ignore a11y-click-events-have-key-events -->
  <!-- svelte-ignore a11y-no-static-element-interactions -->
  <div class="mobile-menu glass-panel" on:click={() => isMobileMenuOpen = false}>
    <a href="/" class="mobile-link">Início</a>
    <a href="/our-values" class="mobile-link">Nossos Valores</a>
    <a href={instagramUrl} target="_blank" class="btn-primary" style="margin-top: 1rem;">Comprar</a>
  </div>
{/if}

<style>
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
    transition:
      opacity 0.3s ease,
      transform 0.3s ease;
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
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1rem;
    transition: font-size 0.3s;
  }

  .vine {
    color: var(--color-lavender);
    opacity: 0.7;
    transition:
      opacity 0.3s,
      width 0.3s;
  }

  .vine-left {
    transform: scaleX(-1);
  }

  nav.scrolled .logo {
    font-size: 1.5rem;
  }

  nav.scrolled .vine {
    opacity: 0.4;
    width: 40px;
  }

  .nav-actions {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    gap: 1.5rem;
    flex: 1;
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

    .links,
    .nav-actions {
      justify-content: center;
      width: 100%;
    }

    nav.scrolled .links {
      display: none;
    }
  }
</style>
