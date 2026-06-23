<script lang="ts">
  export let suppliers: any[];
</script>

<section id="suppliers" class="suppliers snap-section">
  <div class="section-title-wrapper">
    <h2>Nossos Fornecedores</h2>
    <p>Obtido eticamente de todo o mundo</p>
    <hr class="separator" />
  </div>

  <div class="suppliers-grid">
    {#each suppliers as supplier}
      <div class="supplier-card glass-panel">
        <h3>{supplier.name}</h3>
        <span class="region">{supplier.region}</span>
        <p>{supplier.description}</p>
      </div>
    {/each}
  </div>

  <slot name="footer" />
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
    padding: 6rem 2rem 0;
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

  .suppliers-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
    width: 100%;
    max-width: 1000px;
    margin-bottom: 4rem;
  }

  .supplier-card {
    padding: 2rem;
    text-align: center;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1rem;
    transition: transform 0.3s;
  }

  .supplier-card:hover {
    transform: scale(1.05);
  }

  .supplier-card h3 {
    margin: 0;
    font-size: 1.4rem;
  }

  .region {
    background: rgba(181, 126, 220, 0.2);
    color: var(--color-lavender-dark);
    padding: 0.3rem 0.8rem;
    border-radius: 12px;
    font-size: 0.85rem;
    font-weight: 600;
  }

  .supplier-card p {
    font-size: 0.95rem;
    line-height: 1.5;
    opacity: 0.9;
  }
</style>
