<script lang="ts">
  export let alternateLink = { href: "/", text: "Início" };
</script>

<footer class="bottom-footer">
  <div class="footer-links">
    <a href={alternateLink.href} class="footer-link">{alternateLink.text}</a>
    <a
      href="https://instagram.com/lavandroyale"
      target="_blank"
      class="footer-link">Contato através do Instagram</a
    >
    <a href="#" class="footer-link">Desenvolvido por</a>
  </div>
  <div class="footer-badges">
    <span class="badge">🌸 Negócio Feminino</span>
  </div>
  <div class="copyright">
    &copy; {new Date().getFullYear()} Lavande Royale. Todos os direitos reservados.
  </div>
</footer>

<style>
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
</style>
