<script lang="ts">
  export let currentHeroImage: string;
</script>

<section id="hero" class="hero snap-section">
  <div class="hero-bg" style="background-image: url('{currentHeroImage}')"></div>
  <div class="hero-overlay"></div>
  <div class="hero-content">
    <h1 class="hero-title">Elegância em Cada Detalhe</h1>
    <p>Descubra coleções olfativas que despertam no mundo moderno.</p>
  </div>
  <div class="hero-bottom">
    <a href="#home-page" class="aromas-btn" aria-label="Role para Aromas">
      Nossos Aromas
      <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 5v14M19 12l-7 7-7-7" /></svg>
    </a>
  </div>
</section>

<style>
  .snap-section {
    height: 100vh;
    scroll-snap-align: start;
    width: 100%;
  }

  .hero {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  .hero-bg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-size: cover;
    background-position: center;
    filter: blur(4px) saturate(0.8);
    transform: scale(1.05);
    -webkit-mask-image: linear-gradient(to bottom, black 0%, black 40%, transparent 100%);
    mask-image: linear-gradient(to bottom, black 0%, black 40%, transparent 100%);
  }

  .hero-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: radial-gradient(
      circle at center,
      rgba(0, 0, 0, 0.6) 0%,
      rgba(0, 0, 0, 0.2) 100%
    );
    -webkit-mask-image: linear-gradient(to bottom, black 0%, black 40%, transparent 100%);
    mask-image: linear-gradient(to bottom, black 0%, black 40%, transparent 100%);
  }

  .hero-content {
    position: relative;
    z-index: 10;
    max-width: 800px;
    text-align: center;
    padding: 2rem;
    animation: fadeIn 1s ease-out;
    margin-top: -5vh;
  }

  .hero-title {
    font-size: 4.5rem;
    margin-bottom: 1rem;
    color: white;
    text-shadow: 0 4px 30px rgba(0, 0, 0, 0.8), 0 0 10px rgba(0, 0, 0, 0.5);
  }

  .hero-content p {
    font-size: 1.25rem;
    color: white;
    opacity: 0.95;
    max-width: 600px;
    margin: 0 auto;
    font-weight: 500;
    text-shadow: 0 2px 10px rgba(0, 0, 0, 0.6);
  }

  .hero-bottom {
    position: absolute;
    bottom: 2rem;
    left: 50%;
    transform: translateX(-50%);
    z-index: 10;
    text-align: center;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    animation: fadeIn 1.5s ease-out;
  }

  .aromas-btn {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.8rem 1.8rem;
    border-radius: 30px;
    background: var(--color-lavender-light);
    color: var(--color-lavender-dark);
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 1.5px;
    font-size: 1rem;
    transition: all 0.3s;
    animation: bounce 2s infinite;
    box-shadow: 0 4px 15px rgba(181, 126, 220, 0.4);
  }

  .aromas-btn:hover {
    background: var(--color-lavender);
    color: white;
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(181, 126, 220, 0.6);
  }

  @keyframes bounce {
    0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
    40% { transform: translateY(-10px); }
    60% { transform: translateY(-5px); }
  }
  
  @media (max-width: 768px) {
    .hero-title {
      font-size: 2.5rem;
    }
    .hero-content p {
      font-size: 1rem;
    }
    .hero-content {
      padding: 1rem;
    }
    .aromas-btn {
      padding: 0.6rem 1.4rem;
      font-size: 0.9rem;
    }
  }
</style>
