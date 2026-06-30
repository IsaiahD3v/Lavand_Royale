<script lang="ts">
  import Hero from './components/home/Hero.svelte';
  import Carousel from './components/home/Carousel.svelte';
  import PerfumeModal from './components/home/PerfumeModal.svelte';
  import Footer from './components/Footer.svelte';

  const originalPerfumes = [
    { src: "./images/Aether — A Essência que Eleva a Sua Presença.png", name: "Aether — A Essência que Eleva a Sua Presença" },
    { src: "./images/Armaf Infinity Gold.png", name: "Armaf Infinity Gold" },
    { src: "./images/Club de Nuit Iconic.png", name: "Club de Nuit Iconic" },
    { src: "./images/Club de Nuit Woman.png", name: "Club de Nuit Woman" },
    { src: "./images/Delilah Blanc.png", name: "Delilah Blanc" },
    { src: "./images/Nebras.png", name: "Nebras" },
    { src: "./images/power.png", name: "Power" },
  ];

  const perfumes = [...originalPerfumes, ...originalPerfumes];
  let currentHeroImage = "./images/Lavande Royale Hero.png";

  let isPaused = false;
  let selectedPerfume: { src: string; name: string } | null = null;
  let isModalClosing = false;

  function openPerfume(perfume: { src: string; name: string }) {
    selectedPerfume = perfume;
    isPaused = true;
    document.body.classList.add("modal-open");
  }

  async function closePerfume() {
    isModalClosing = true;
    setTimeout(() => {
      selectedPerfume = null;
      isModalClosing = false;
      isPaused = false;
      document.body.classList.remove("modal-open");
    }, 400);
  }

  function getInstagramUrl() {
    return `https://instagram.com/lavandroyale`;
  }
</script>

<Hero {currentHeroImage} />

<Carousel {perfumes} {originalPerfumes} {isPaused} {openPerfume} />

<div class="footer-snap">
  <Footer alternateLink={{ href: '/our-values', text: 'Nossos Valores' }} />
</div>

{#if selectedPerfume}
  <PerfumeModal {selectedPerfume} {isModalClosing} {closePerfume} {getInstagramUrl} />
{/if}

<style>
  .footer-snap {
    scroll-snap-align: end;
    width: 100%;
  }
</style>
