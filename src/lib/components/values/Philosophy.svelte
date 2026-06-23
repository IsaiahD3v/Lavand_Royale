<script lang="ts">
</script>

<section id="philosophy" class="philosophy snap-section">
  <div class="content-box glass-panel">
    <h2>Nossa Filosofia</h2>
    <p class="lead">Um delicado equilíbrio entre a natureza e a sofisticação moderna.</p>
    <p>
      Na Lavand Royale, acreditamos que a verdadeira elegância está nos detalhes. 
      Nós nos esforçamos para criar aromas que não sejam apenas aromas, mas experiências—criadas 
      com o maior respeito pelo meio ambiente e uma paixão pela beleza minimalista. 
      Nossa mistura exclusiva de lavanda pálida e cinza profundo reflete nosso compromisso com 
      o design atemporal e sofisticado.
    </p>
  </div>
  <div class="scroll-indicator">
    <p>Depoimentos</p>
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 5v14M19 12l-7 7-7-7"/></svg>
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

  .content-box {
    max-width: 800px;
    padding: 3rem;
    text-align: center;
  }

  .content-box h2 {
    font-size: 3rem;
    color: var(--color-lavender);
    margin-bottom: 1.5rem;
  }

  .lead {
    font-size: 1.5rem;
    font-weight: 600;
    margin-bottom: 1.5rem;
    color: var(--color-lavender-dark);
  }

  .content-box p:not(.lead) {
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
    gap: 0.5rem;
    opacity: 0.6;
    animation: pulse 2s infinite;
  }

  @keyframes pulse {
    0%, 100% { opacity: 0.4; transform: translateY(0); }
    50% { opacity: 1; transform: translateY(5px); }
  }

  @media (max-width: 768px) {
    .content-box {
      padding: 2rem;
    }
    .content-box h2 {
      font-size: 2.5rem;
    }
  }
</style>
