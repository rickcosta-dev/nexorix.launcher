<script>
  import { t } from '$lib/i18n.js';
  const year = new Date().getFullYear();
</script>

<footer>
  <div class="container">
    <div class="top">
      <div class="brand">
        <div class="logo"><span>N</span>EXORIX</div>
        <p>{$t.footerBrand}</p>
      </div>

      <div class="links-group">
        <div class="link-col">
          <div class="col-title">{$t.footerNav}</div>
          <a href="#features">{$t.nav.features}</a>
          <a href="#tech">{$t.nav.tech}</a>
          <a href="#developer">{$t.nav.dev}</a>
          <a href="#download">{$t.nav.download}</a>
        </div>
        <div class="link-col">
          <div class="col-title">{$t.footerLinks}</div>
          <a href="https://github.com/rickcosta-dev" target="_blank" rel="noopener">GitHub</a>
          <a href="https://discord.com/users/917890301547393024" target="_blank" rel="noopener">Discord</a>
        </div>
      </div>
    </div>

    <div class="bottom">
      <span>© {year} NEXORIX Launcher · {$t.footerCredit} <strong>RickZIn021</strong></span>
      <span class="built-with">
        {$t.builtWith}
        <span class="heart">♥</span>
        {$t.builtIn}
      </span>
    </div>
  </div>
</footer>

<style>
  footer {
    border-top: 1px solid var(--border);
    padding: 3rem 0 2rem;
    position: relative;
    z-index: 1;
  }
  .container {
    width: 100%;
    max-width: var(--max-w);
    margin: 0 auto;
    padding: 0 var(--pad);
  }

  .top {
    display: flex;
    justify-content: space-between;
    gap: 3rem;
    margin-bottom: 2.5rem;
    flex-wrap: wrap;
  }

  .brand { max-width: 280px; }
  .logo {
    font-size: 1.2rem;
    font-weight: 900;
    letter-spacing: 0.05em;
    margin-bottom: 0.75rem;
  }
  .logo span { color: var(--accent); }
  .brand p { font-size: 0.85rem; color: var(--text-muted); line-height: 1.6; }

  .links-group { display: flex; gap: 3rem; }
  .link-col { display: flex; flex-direction: column; gap: 0.5rem; }
  .col-title {
    font-size: 0.75rem;
    font-weight: 700;
    color: var(--text-muted);
    text-transform: uppercase;
    letter-spacing: 0.08em;
    margin-bottom: 0.25rem;
  }
  .link-col a {
    font-size: 0.85rem;
    color: var(--text-dim);
    text-decoration: none;
    transition: color 0.2s;
  }
  .link-col a:hover { color: var(--text); }

  .bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 0.5rem;
    padding-top: 1.5rem;
    border-top: 1px solid var(--border);
    font-size: 0.8rem;
    color: var(--text-muted);
  }
  .bottom strong { color: var(--accent); }
  .built-with { display: flex; align-items: center; gap: 0.3rem; }
  .heart { color: #f44; animation: heartbeat 1.5s ease infinite; }
  @keyframes heartbeat {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.2); }
  }

  @media (max-width: 640px) {
    .links-group { gap: 2rem; }
    .bottom { flex-direction: column; text-align: center; }
  }
</style>
