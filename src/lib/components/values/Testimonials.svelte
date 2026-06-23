<script lang="ts">
  export let testimonials: any[];
</script>

<section id="testimonials" class="testimonials snap-section">
  <div class="section-title-wrapper">
    <h2>Depoimentos</h2>
    <p>O que nossos clientes dizem</p>
    <hr class="separator" />
  </div>

  <div class="testimonials-list">
    {#each testimonials as review}
      <div class="testimonial-card glass-panel">
        <div class="stars">{"★".repeat(review.rating)}{"☆".repeat(5-review.rating)}</div>
        <p class="quote">"{review.quote}"</p>
        <p class="author">- {review.author}</p>
      </div>
    {/each}
  </div>
</section>

<style>
  .snap-section {
    height: 100vh;
    scroll-snap-align: start;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: relative;
    padding: 6rem 2rem 2rem;
  }

  .section-title-wrapper {
    text-align: center;
    margin-bottom: 3rem;
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

  .testimonials-list {
    display: flex;
    gap: 2rem;
    flex-wrap: wrap;
    justify-content: center;
    max-width: 1200px;
  }

  .testimonial-card {
    flex: 1 1 300px;
    max-width: 350px;
    padding: 2rem;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    transition: transform 0.3s;
  }

  .testimonial-card:hover {
    transform: translateY(-5px);
  }

  .stars {
    color: var(--color-lavender);
    font-size: 1.2rem;
  }

  .quote {
    font-style: italic;
    line-height: 1.6;
    flex-grow: 1;
  }

  .author {
    font-weight: 600;
    text-align: right;
    color: var(--color-lavender-dark);
  }

  .scroll-indicator {
    position: absolute;
    bottom: 2rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    opacity: 0.6;
    animation: pulse 2s infinite;
  }

  @keyframes pulse {
    0%, 100% { opacity: 0.4; transform: translateY(0); }
    50% { opacity: 1; transform: translateY(5px); }
  }

  @media (max-width: 768px) {
    .section-title-wrapper h2 {
      font-size: 2rem;
    }
    .testimonials-list {
      flex-wrap: nowrap;
      overflow-x: auto;
      scroll-snap-type: x mandatory;
      justify-content: flex-start;
      padding-bottom: 1.5rem;
      width: 100vw;
      padding-left: 5vw;
      padding-right: 5vw;
      -webkit-overflow-scrolling: touch;
    }
    .testimonial-card {
      scroll-snap-align: center;
      flex: 0 0 85%;
      max-width: 85%;
    }
    /* Hide scrollbar for cleaner look */
    .testimonials-list::-webkit-scrollbar {
      display: none;
    }
    .testimonials-list {
      -ms-overflow-style: none;
      scrollbar-width: none;
    }
  }
</style>
