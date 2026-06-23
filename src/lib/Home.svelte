<script lang="ts">
  const originalImages = [
    '/images/{3535DF3A-B038-4BFE-AE21-A6D02FFC1A30}.png',
    '/images/{43AF1846-4AD4-4DE9-A18A-1ECFB11AD457}.png',
    '/images/{65BA7E79-C137-4D35-896E-F888AE5407D6}.png',
    '/images/{66A1B26C-EDD7-4E81-A217-C471F6EFC82A}.png',
    '/images/{73DCF913-4E8F-4B09-B294-2294F78B8281}.png',
    '/images/{8D484B2F-2506-4E8C-93D9-9D705D324E90}.png',
    '/images/{90E7774E-72BE-4307-8BC7-69F9111FD89F}.png',
    '/images/{B0B4E745-5DFB-41ED-BE4E-AAE0DCBC4957}.png',
    '/images/{B7602C43-26D9-497D-9B07-6769EDFF2610}.png',
    '/images/{FE0B62C9-B82A-4751-805A-9E362BF4AA64}.png'
  ];
  
  const images = [...originalImages, ...originalImages];
  let currentHeroImage = originalImages[1];
  
  let isPaused = false;
  let selectedPerfume: { img: string, index: number } | null = null;
  let isModalClosing = false;

  function openPerfume(img: string, index: number) {
    const realIndex = index % originalImages.length;
    selectedPerfume = { img, index: realIndex };
    isPaused = true;
    document.body.classList.add('modal-open');
  }

  async function closePerfume() {
    isModalClosing = true;
    setTimeout(() => {
      selectedPerfume = null;
      isModalClosing = false;
      isPaused = false;
      document.body.classList.remove('modal-open');
    }, 400);
  }

  function getWhatsAppUrl(perfumeName: string) {
    const message = encodeURIComponent(`Hello, I'm interested in ${perfumeName} from Lavand Royale.`);
    return `https://wa.me/?text=${message}`;
  }
</script>

<!-- Section 1: Hero -->
<section id="hero" class="hero snap-section">
  <div class="hero-bg" style="background-image: url('{currentHeroImage}')"></div>
  <div class="hero-overlay"></div>
  <div class="hero-content">
    <h1 class="hero-title">Elegance in Every Detail</h1>
    <p>Discover the new Lavand Royale collection. A symphony of lavender and grey, designed for the modern aesthetic.</p>
  </div>
  <div class="hero-bottom">
    <p class="aromas-text">Our Aromas</p>
    <a href="#carousel-section" class="scroll-down-btn" aria-label="Scroll to Aromas">
      <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 5v14M19 12l-7 7-7-7"/></svg>
    </a>
  </div>
</section>

<!-- Section 2: Carousel -->
<section id="carousel-section" class="carousel-section snap-section">
  <div class="section-title-wrapper">
    <h2>Curated Selections</h2>
    <p>Immerse yourself in our signature pieces</p>
    <hr class="separator" />
  </div>
  
  <div class="carousel-track-wrapper">
    <div class="carousel-track" class:paused={isPaused}>
      {#each images as img, i}
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <!-- svelte-ignore a11y-no-static-element-interactions -->
        <div class="carousel-item" on:click={() => openPerfume(img, i)}>
          <img src={img} alt="" class="ambient-glow" />
          <img src={img} alt="Perfume Bottle {(i % originalImages.length) + 1}" class="main-image" />
          
          <div class="item-overlay glass-panel">
            <h3>Signature {(i % originalImages.length) + 1}</h3>
            <span>Click to View</span>
          </div>
        </div>
      {/each}
    </div>
  </div>

  <footer class="bottom-footer">
    <div class="footer-links">
      <a href="/our-values" class="footer-link">Our Values</a>
      <a href="https://instagram.com/lavandroyale" target="_blank" class="footer-link">Instagram Contact</a>
      <a href="#" class="footer-link">Made by Lavand</a>
    </div>
    <div class="footer-badges">
      <span class="badge">🌸 Feminine Business</span>
    </div>
    <div class="copyright">
      &copy; {new Date().getFullYear()} Lavand Royale. All rights reserved.
    </div>
  </footer>
</section>

<!-- Modal for Perfume Details -->
{#if selectedPerfume}
  <div class="modal-backdrop {isModalClosing ? 'closing' : ''}" on:click={closePerfume}></div>
  <div class="modal-content {isModalClosing ? 'closing' : ''} glass-panel">
    <button class="close-btn" on:click={closePerfume}>&times;</button>
    
    <div class="modal-body">
      <div class="modal-image-container">
        <img src={selectedPerfume.img} alt="" class="ambient-glow" />
        <img src={selectedPerfume.img} alt="Signature {selectedPerfume.index + 1}" class="main-image" />
      </div>
      
      <div class="modal-info">
        <h2>Signature Aroma {selectedPerfume.index + 1}</h2>
        <p class="description">
          A captivating blend of wild lavender, subtle citrus notes, and a deep grey musk base. 
          This signature aroma is crafted for those who appreciate the delicate balance of nature and modern sophistication.
        </p>
        <div class="modal-actions">
          <a href={getWhatsAppUrl(`Signature Aroma ${selectedPerfume.index + 1}`)} target="_blank" class="btn-whatsapp">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M11.99 2C6.47 2 2 6.48 2 12c0 1.77.46 3.44 1.28 4.9L2 22l5.24-1.24A9.974 9.974 0 0012 22c5.52 0 10-4.48 10-10S17.51 2 11.99 2zm5.72 14.19c-.24.68-1.4 1.25-1.93 1.34-.41.07-.94.13-2.61-.53-2.02-.79-3.32-2.88-3.42-3.02-.1-.13-.82-1.09-.82-2.08 0-.99.51-1.48.69-1.68.18-.2.39-.25.52-.25.13 0 .26.01.38.02.14.01.32-.05.49.35.18.42.6 1.46.65 1.56.05.1.09.22.02.35-.07.13-.11.21-.21.32-.1.11-.22.25-.3.34-.1.1-.21.22-.09.43.12.21.53.88 1.13 1.41.77.68 1.43.89 1.64.99.21.1.33.08.45-.06.13-.14.54-.62.69-.83.15-.21.3-.18.49-.11.2.07 1.26.59 1.47.7.21.11.36.16.41.25.05.09.05.51-.19 1.19z"/></svg>
            Contact on WhatsApp
          </a>
        </div>
      </div>
    </div>
  </div>
{/if}

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
  }

  .hero-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(180deg, rgba(0,0,0, 0.4) 0%, transparent 100%);
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
    background: linear-gradient(135deg, var(--color-lavender-light), var(--color-lavender));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    text-shadow: 0 4px 20px rgba(0,0,0,0.1);
  }

  .hero-content p {
    font-size: 1.25rem;
    color: var(--color-text);
    opacity: 0.9;
    max-width: 600px;
    margin: 0 auto;
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

  .aromas-text {
    font-size: 1.2rem;
    font-weight: 700;
    letter-spacing: 2px;
    text-transform: uppercase;
    margin: 0;
    color: var(--color-lavender);
  }

  .scroll-down-btn {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background: rgba(255,255,255,0.1);
    backdrop-filter: blur(5px);
    border: 1px solid rgba(255,255,255,0.2);
    color: var(--color-text);
    transition: all 0.3s;
    animation: bounce 2s infinite;
  }

  .scroll-down-btn:hover {
    background: var(--color-lavender);
    color: white;
    border-color: var(--color-lavender);
  }

  @keyframes bounce {
    0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
    40% { transform: translateY(-10px); }
    60% { transform: translateY(-5px); }
  }

  /* Carousel Section */
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
    background: linear-gradient(90deg, transparent, var(--color-lavender), transparent);
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

  .carousel-item,
  .modal-image-container {
    position: relative;
    border-radius: var(--border-radius);
    overflow: hidden;
    background: transparent;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1;
  }

  .carousel-item {
    width: 300px;
    height: 400px;
    cursor: pointer;
    box-shadow: var(--box-shadow);
    transition: transform 0.4s cubic-bezier(0.25, 0.8, 0.25, 1);
  }

  .modal-image-container {
    flex: 1;
    height: 450px;
    box-shadow: inset 0 0 20px rgba(0,0,0,0.05);
  }

  .carousel-item:hover {
    transform: translateY(-15px) scale(1.02);
  }

  .ambient-glow {
    position: absolute;
    top: 50%; left: 50%;
    width: 100%; height: 100%;
    transform: translate(-50%, -50%) scale(1.2);
    object-fit: cover;
    filter: blur(40px) saturate(1.8) opacity(0.7);
    z-index: -1;
    pointer-events: none;
  }

  .main-image {
    width: 100%;
    height: 100%;
    object-fit: contain;
    border-radius: inherit; 
    transition: transform 0.6s cubic-bezier(0.25, 0.8, 0.25, 1);
    -webkit-mask-image: radial-gradient(circle at center, black 40%, transparent 95%);
    mask-image: radial-gradient(circle at center, black 40%, transparent 95%);
    position: relative;
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

  .bottom-footer {
    margin-top: auto;
    padding: 3rem 2rem 2rem;
    width: 100%;
    text-align: center;
    background: rgba(0, 0, 0, 0.02);
    border-top: 1px solid rgba(255, 255, 255, 0.05);
  }

  .footer-links {
    display: flex;
    justify-content: center;
    gap: 2rem;
    margin-bottom: 1.5rem;
    flex-wrap: wrap;
  }

  .footer-link {
    font-weight: 600;
    font-size: 1rem;
    color: var(--color-lavender);
    transition: color 0.3s;
  }
  
  .footer-link:hover {
    color: var(--color-lavender-dark);
  }

  .footer-badges {
    margin-bottom: 1.5rem;
  }

  .badge {
    background: var(--color-lavender-light);
    color: var(--color-lavender-dark);
    padding: 0.5rem 1rem;
    border-radius: 20px;
    font-size: 0.85rem;
    font-weight: 700;
    letter-spacing: 1px;
    text-transform: uppercase;
  }

  .copyright {
    opacity: 0.6;
    font-size: 0.9rem;
  }

  /* Modal Styles */
  .modal-backdrop {
    position: fixed;
    top: 0; left: 0; width: 100%; height: 100%;
    background: rgba(0, 0, 0, 0.6);
    backdrop-filter: blur(8px);
    z-index: 2000;
    animation: fadeIn 0.4s cubic-bezier(0.25, 0.8, 0.25, 1);
  }

  .modal-backdrop.closing {
    animation: fadeOut 0.4s cubic-bezier(0.25, 0.8, 0.25, 1) forwards;
  }

  .modal-content {
    position: fixed;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%) scale(1);
    width: 90%; max-width: 900px;
    z-index: 2001;
    border-radius: var(--border-radius);
    padding: 2.5rem;
    animation: popIn 0.4s cubic-bezier(0.25, 0.8, 0.25, 1);
  }

  .modal-content.closing {
    animation: popOut 0.4s cubic-bezier(0.25, 0.8, 0.25, 1) forwards;
  }

  .close-btn {
    position: absolute;
    top: 1.5rem; right: 1.5rem;
    background: rgba(255, 255, 255, 0.4);
    border: none;
    width: 40px; height: 40px;
    border-radius: 50%;
    font-size: 1.5rem;
    color: var(--color-text);
    cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    transition: all 0.2s;
    z-index: 10;
  }

  .close-btn:hover {
    background: var(--color-lavender);
    color: white;
  }

  .modal-body {
    display: flex;
    gap: 3rem;
    align-items: center;
  }

  .modal-info {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
  }

  .modal-info h2 {
    font-size: 2.5rem;
    margin: 0;
    color: var(--color-lavender);
  }

  .modal-info .description {
    font-size: 1.1rem;
    line-height: 1.6;
    opacity: 0.9;
  }

  .modal-actions {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    margin-top: 1rem;
  }

  @keyframes popIn {
    from { opacity: 0; transform: translate(-50%, -50%) scale(0.95); }
    to { opacity: 1; transform: translate(-50%, -50%) scale(1); }
  }

  @keyframes popOut {
    from { opacity: 1; transform: translate(-50%, -50%) scale(1); }
    to { opacity: 0; transform: translate(-50%, -50%) scale(0.95); }
  }

  @keyframes fadeOut {
    from { opacity: 1; }
    to { opacity: 0; }
  }

  @media (max-width: 768px) {
    .hero-title {
      font-size: 3rem;
    }
    .modal-body {
      flex-direction: column;
    }
    .modal-image-container {
      height: 250px;
      width: 100%;
    }
    .carousel-item {
      width: 260px;
      height: 350px;
    }
  }
</style>
