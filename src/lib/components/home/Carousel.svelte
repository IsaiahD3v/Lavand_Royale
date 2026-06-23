<script lang="ts">
  export let perfumes: { src: string; name: string }[];
  export let originalPerfumes: { src: string; name: string }[];
  export let isPaused: boolean;
  export let openPerfume: (perfume: { src: string; name: string }) => void;
</script>

<section id="home-page" class="carousel-section snap-section">
  <div class="section-title-wrapper">
    <h2>Seleções Especiais</h2>
    <p>Mergulhe nas nossas peças exclusivas</p>
    <hr class="separator" />
  </div>

  <div class="carousel-track-wrapper">
    <div class="carousel-track" class:paused={isPaused}>
      {#each perfumes as perfume}
        <div
          class="carousel-item"
          on:click={() => openPerfume(perfume)}
          role="button"
          tabindex="0"
          on:keydown={(e) => e.key === 'Enter' && openPerfume(perfume)}
        >
          <img src={perfume.src} alt={perfume.name} class="ambient-glow" />
          <img
            src={perfume.src}
            alt={perfume.name}
            class="main-image"
          />

          <div class="item-overlay glass-panel">
            <h3>{perfume.name}</h3>
            <span>Clique para Ver</span>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>

<style>
  .snap-section {
    height: 100vh;
    scroll-snap-align: start;
    width: 100%;
  }

  .carousel-section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    position: relative;
    padding-top: 4rem;
  }

  .section-title-wrapper {
    text-align: center;
    margin-bottom: 2rem;
    width: 80%;
    max-width: 800px;
  }

  .section-title-wrapper h2 {
    font-size: 2.5rem;
    color: var(--color-lavender);
    margin-bottom: 0.5rem;
  }

  .separator {
    border: 0;
    height: 1px;
    background: linear-gradient(
      90deg,
      transparent,
      var(--color-lavender),
      transparent
    );
    margin: 1.5rem auto;
    width: 50%;
  }

  .carousel-track-wrapper {
    width: 100%;
    overflow: hidden;
    padding: 2rem 0;
  }

  .carousel-track {
    display: flex;
    gap: 2rem;
    width: max-content;
    animation: scrollLeft 70s linear infinite;
  }

  .carousel-track.paused {
    animation-play-state: paused;
  }

  @keyframes scrollLeft {
    0% { transform: translateX(0); }
    100% { transform: translateX(calc(-50% - 1rem)); }
  }

  .carousel-item {
    flex: 0 0 auto;
    width: 280px;
    height: 400px;
    border-radius: var(--border-radius);
    overflow: hidden;
    position: relative;
    cursor: pointer;
    transition: transform 0.4s cubic-bezier(0.25, 0.8, 0.25, 1);
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  }

  /* Liquid glass highlight */
  .carousel-item::after {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0; bottom: 0;
    border-radius: inherit;
    pointer-events: none;
    z-index: 3;
    background: linear-gradient(135deg, rgba(255,255,255,0.7) 0%, rgba(255,255,255,0.2) 20%, rgba(255,255,255,0) 50%);
    box-shadow: 
      inset 0 0 0 1px rgba(255,255,255,0.3), 
      inset 0 1px 1px rgba(255,255,255,0.9), 
      inset 1px 0 1px rgba(255,255,255,0.6), 
      inset 0 20px 40px rgba(255,255,255,0.3);
  }

  .carousel-item:hover {
    transform: scale(1.05) translateY(-10px);
    box-shadow: 0 20px 40px rgba(181, 126, 220, 0.3);
  }

  .ambient-glow {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    transform: scale(1.1);
    object-fit: cover;
    filter: blur(40px) saturate(2);
    opacity: 0.5;
    z-index: 0;
  }

  .main-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    position: relative;
    z-index: 1;
    transition: transform 0.6s cubic-bezier(0.25, 0.8, 0.25, 1);
    z-index: 0;
  }

  .carousel-item:hover .main-image {
    transform: scale(1.08);
  }

  .item-overlay {
    position: absolute;
    bottom: -100%;
    left: 1rem;
    right: 1rem;
    padding: 1rem;
    transition: bottom 0.4s cubic-bezier(0.25, 0.8, 0.25, 1);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    z-index: 2;
  }

  .carousel-item:hover .item-overlay {
    bottom: 1rem;
  }

  .item-overlay h3 {
    margin: 0;
    font-size: 1.2rem;
    color: var(--color-lavender-dark);
  }

  .item-overlay span {
    font-size: 0.9rem;
    font-weight: 600;
  }

  @media (max-width: 768px) {
    .carousel-item {
      width: 240px;
      height: 340px;
    }
    .section-title-wrapper h2 {
      font-size: 2rem;
    }
    .section-title-wrapper {
      margin-bottom: 1rem;
    }
    .carousel-track-wrapper {
      padding: 1rem 0;
    }
    .item-overlay {
      bottom: 1rem;
      padding: 0.8rem;
    }
    .item-overlay h3 {
      font-size: 1rem;
    }
    .item-overlay span {
      display: none;
    }
  }
</style>
