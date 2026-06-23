<script lang="ts">
  export let selectedPerfume: { src: string; name: string };
  export let isModalClosing: boolean;
  export let closePerfume: () => void;
  export let getInstagramUrl: () => string;
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
<div class="modal-backdrop {isModalClosing ? 'closing' : ''}" on:click={closePerfume} role="presentation"></div>
<div class="modal-content {isModalClosing ? 'closing' : ''} glass-panel">
  <img src={selectedPerfume.src} alt="" class="ambient-glow" />
  <button class="close-btn" on:click={closePerfume}>&times;</button>

  <div class="modal-body">
    <div class="modal-image-container">
      <img
        src={selectedPerfume.src}
        alt={selectedPerfume.name}
        class="main-image"
      />
    </div>

    <div class="modal-info">
      <h2>{selectedPerfume.name}</h2>
      <p class="description">
        Uma mistura cativante de lavanda selvagem, notas cítricas sutis e uma base profunda de almíscar cinza. Este aroma assinatura é criado para aqueles que apreciam o delicado equilíbrio entre a natureza e a sofisticação moderna.
      </p>
      <div class="modal-actions">
        <a
          href={getInstagramUrl()}
          target="_blank"
          class="btn-instagram"
        >
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect><path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path><line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line></svg>
          Contato pelo Instagram
        </a>
      </div>
    </div>
  </div>
</div>

<style>
  .modal-backdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
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
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(1);
    width: 90%;
    max-width: 900px;
    z-index: 2001;
    border-radius: var(--border-radius);
    padding: 2.5rem;
    overflow: hidden;
    animation: popIn 0.4s cubic-bezier(0.25, 0.8, 0.25, 1);
  }

  .modal-content.closing {
    animation: popOut 0.4s cubic-bezier(0.25, 0.8, 0.25, 1) forwards;
  }

  .close-btn {
    position: absolute;
    top: 1.5rem;
    right: 1.5rem;
    background: rgba(255, 255, 255, 0.4);
    border: none;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    font-size: 1.5rem;
    color: var(--color-text);
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
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
  
  .modal-image-container {
    position: relative;
    border-radius: var(--border-radius);
    overflow: hidden;
    background: transparent;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1;
    flex: 1;
    height: 450px;
  }
  
  .ambient-glow {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    transform: scale(1.1);
    object-fit: cover;
    filter: blur(80px) saturate(2);
    opacity: 0.4;
    z-index: -1;
    pointer-events: none;
  }

  .main-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: inherit;
    -webkit-mask-image: radial-gradient(
      ellipse at center,
      black 30%,
      transparent 80%
    );
    mask-image: radial-gradient(ellipse at center, black 30%, transparent 80%);
    position: relative;
    z-index: 0;
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
    color: white;
  }

  .modal-info .description {
    font-size: 1.1rem;
    line-height: 1.6;
    opacity: 0.9;
    color: white;
  }

  .modal-actions {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    margin-top: 1rem;
  }

  @keyframes popIn {
    from {
      opacity: 0;
      transform: translate(-50%, -50%) scale(0.95);
    }
    to {
      opacity: 1;
      transform: translate(-50%, -50%) scale(1);
    }
  }

  @keyframes popOut {
    from {
      opacity: 1;
      transform: translate(-50%, -50%) scale(1);
    }
    to {
      opacity: 0;
      transform: translate(-50%, -50%) scale(0.95);
    }
  }

  @keyframes fadeOut {
    from { opacity: 1; }
    to { opacity: 0; }
  }

  @media (max-width: 768px) {
    .modal-content {
      width: 95%;
      padding: 1.5rem;
      max-height: 90vh;
      overflow-y: auto;
    }
    .modal-body {
      flex-direction: column;
      gap: 1.5rem;
    }
    .modal-image-container {
      height: 250px;
      width: 100%;
    }
    .modal-info h2 {
      font-size: 1.8rem;
    }
    .modal-info .description {
      font-size: 1rem;
    }
    .close-btn {
      top: 0.5rem;
      right: 0.5rem;
      width: 35px;
      height: 35px;
    }
  }
</style>
