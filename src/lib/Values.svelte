<script lang="ts">
  const testimonials = [
    { name: "Eleanor V.", text: "The most delicate and sophisticated aromas I've ever experienced. A true masterpiece." },
    { name: "Julian M.", text: "Lavand Royale perfectly captures the essence of modern elegance. It's my daily signature." },
    { name: "Sophia R.", text: "From the glass bottle to the subtle notes of lavender, everything is crafted with perfection." }
  ];

  const suppliers = [
    { name: "Provence Lavender Co.", detail: "Ethically sourced wild lavender from the heart of France." },
    { name: "Aethel Glassworks", detail: "Hand-blown, sustainable glass bottles crafted by artisans." },
    { name: "Essence Extractors", detail: "Cold-press extraction preserving the purest aromatic oils." }
  ];
</script>

<div class="values-container">
  <!-- Section 1: Philosophy -->
  <section id="philosophy" class="philosophy snap-section">
    <div class="content-box glass-panel">
      <h2>Our Philosophy</h2>
      <p class="lead">A delicate balance between nature and modern sophistication.</p>
      <p>
        At Lavand Royale, we believe that true elegance lies in the details. 
        We strive to create aromas that are not just scents, but experiences—crafted 
        with the utmost respect for the environment and a passion for minimalist beauty. 
        Our signature blend of pale lavender and deep grey reflects our commitment to 
        timeless, sophisticated design.
      </p>
    </div>
    <div class="scroll-indicator">
      <p>Suppliers</p>
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 5v14M19 12l-7 7-7-7"/></svg>
    </div>
  </section>

  <!-- Section 2: Testimonials -->
  <section id="testimonials" class="testimonials snap-section">
    <div class="section-title-wrapper">
      <h2>Testimonials</h2>
      <p>What our clients say</p>
      <hr class="separator" />
    </div>

    <div class="testimonials-list">
      {#each testimonials as review}
        <div class="testimonial-card glass-panel">
          <p class="quote">"{review.text}"</p>
          <p class="author">- {review.name}</p>
        </div>
      {/each}
    </div>
  </section>

  <!-- Section 3: Suppliers -->
  <section id="suppliers" class="suppliers snap-section">
    <div class="section-title-wrapper">
      <h2>Our Suppliers</h2>
      <p>Transparency and ethical sourcing</p>
      <hr class="separator" />
    </div>

    <div class="suppliers-grid">
      {#each suppliers as supplier}
        <div class="supplier-card glass-panel">
          <h3>{supplier.name}</h3>
          <p>{supplier.detail}</p>
        </div>
      {/each}
    </div>

    <footer class="bottom-footer">
      <div class="footer-links">
        <a href="/" class="footer-link">Home</a>
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
</div>

<style>
  .values-container {
    padding-top: 2rem;
  }

  .snap-section {
    height: 100vh;
    scroll-snap-align: start;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: relative;
  }

  .section-title-wrapper {
    text-align: center;
    margin-bottom: 3rem;
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

  /* Philosophy */
  .philosophy {
    background: radial-gradient(circle at center, var(--color-lavender-light) 0%, transparent 60%);
  }

  .content-box {
    max-width: 800px;
    padding: 3rem 4rem;
    text-align: center;
  }

  .content-box h2 {
    font-size: 3rem;
    color: var(--color-lavender);
    margin-bottom: 1rem;
  }

  .content-box .lead {
    font-size: 1.4rem;
    font-weight: 600;
    margin-bottom: 1.5rem;
    color: var(--color-lavender-dark);
  }

  .content-box p {
    font-size: 1.1rem;
    line-height: 1.8;
    color: var(--color-text);
    opacity: 0.9;
  }

  .scroll-indicator {
    position: absolute;
    bottom: 2rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    color: var(--color-lavender);
    font-weight: 600;
    animation: bounce 2s infinite;
  }

  @keyframes bounce {
    0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
    40% { transform: translateY(-10px); }
    60% { transform: translateY(-5px); }
  }

  /* Suppliers */
  .suppliers-grid {
    display: flex;
    gap: 2rem;
    flex-wrap: wrap;
    justify-content: center;
    max-width: 1000px;
    padding: 0 2rem;
  }

  .supplier-card {
    flex: 1;
    min-width: 250px;
    padding: 2rem;
    text-align: center;
    transition: transform 0.3s;
  }

  .supplier-card:hover {
    transform: translateY(-10px);
  }

  .supplier-card h3 {
    color: var(--color-lavender-dark);
    margin-bottom: 1rem;
    font-size: 1.3rem;
  }

  /* Testimonials */
  .testimonials-list {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
    width: 90%;
    max-width: 800px;
  }

  .testimonial-card {
    padding: 2rem;
    border-left: 4px solid var(--color-lavender);
  }

  .quote {
    font-size: 1.2rem;
    font-style: italic;
    margin-bottom: 1rem;
    opacity: 0.9;
  }

  .author {
    font-weight: 700;
    color: var(--color-lavender-dark);
    text-align: right;
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

  @media (max-width: 768px) {
    .content-box {
      padding: 2rem;
    }
    .content-box h2 {
      font-size: 2.2rem;
    }
  }
</style>
