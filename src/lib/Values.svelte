<script lang="ts">
  import Philosophy from './components/values/Philosophy.svelte';
  import Testimonials from './components/values/Testimonials.svelte';
  import Footer from './components/Footer.svelte';

  const testimonials = [
    {
      quote: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
      author: "Cliente 1",
      rating: 5
    },
    {
      quote: "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
      author: "Cliente 2",
      rating: 5
    },
    {
      quote: "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
      author: "Cliente 3",
      rating: 4
    }
  ];
</script>

<div class="values-container">
  <Philosophy />
  <Testimonials {testimonials} />
</div>

<div class="footer-snap">
  <Footer alternateLink={{ href: '/', text: 'Início' }} />
</div>

<style>
  .values-container {
    width: 100%;
  }

  .footer-snap {
    scroll-snap-align: end;
    width: 100%;
  }
</style>
