<script>
  import { onMount } from 'svelte';
  import { t, currentLang, langs } from '$lib/i18n.js';

  let scrolled = false;
  let showLangMenu = false;

  onMount(() => {
    const handler = () => { scrolled = window.scrollY > 40; };
    window.addEventListener('scroll', handler, { passive: true });
    const close = (e) => { if (!e.target.closest('.lang-picker')) showLangMenu = false; };
    document.addEventListener('click', close);
    return () => {
      window.removeEventListener('scroll', handler);
      document.removeEventListener('click', close);
    };
  });

  function setLang(lang) {
    currentLang.set(lang);
    showLangMenu = false;
  }

  const flagMap = {
    'Português': '🇧🇷',
    'English':   '🇺🇸',
    'Español':   '🇪🇸',
    'Русский':   '🇷🇺',
    'Deutsch':   '🇩🇪',
  };
</script>

<nav class:scrolled>
  <div class="inner">
    <a href="/" class="logo">
      <span class="logo-n">N</span>EXORIX
    </a>

    <ul class="links">
      <li><a href="#features">{$t.nav.features}</a></li>
      <li><a href="#tech">{$t.nav.tech}</a></li>
      <li><a href="#developer">{$t.nav.dev}</a></li>

      <!-- Language picker -->
      <li class="lang-picker">
        <button class="lang-btn" on:click|stopPropagation={() => showLangMenu = !showLangMenu}>
          <span>{flagMap[$currentLang]}</span>
          <span class="lang-name">{$currentLang}</span>
          <svg width="10" height="10" viewBox="0 0 10 10" fill="currentColor" style="opacity:0.5">
            <path d="M1 3l4 4 4-4"/>
          </svg>
        </button>
        {#if showLangMenu}
          <div class="lang-menu">
            {#each langs as lang}
              <button class="lang-item" class:active={$currentLang === lang}
                      on:click={() => setLang(lang)}>
                <span>{flagMap[lang]}</span>
                <span>{lang}</span>
              </button>
            {/each}
          </div>
        {/if}
      </li>

      <li><a href="#download" class="btn-nav">{$t.nav.download}</a></li>
    </ul>
  </div>
</nav>

<style>
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    padding: 0.85rem 0;
    transition: background 0.3s, backdrop-filter 0.3s, border-color 0.3s;
    border-bottom: 1px solid transparent;
  }
  nav.scrolled {
    background: rgba(13,15,20,0.9);
    backdrop-filter: blur(20px);
    border-color: var(--border);
  }
  .inner {
    width: 100%;
    max-width: 1400px;
    margin: 0 auto;
    padding: 0 3rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .logo {
    font-size: 1.3rem;
    font-weight: 800;
    letter-spacing: 0.05em;
    color: var(--text);
    text-decoration: none;
  }
  .logo-n { color: var(--accent); }

  .links {
    list-style: none;
    display: flex;
    gap: 1.5rem;
    align-items: center;
  }
  .links a {
    color: var(--text-dim);
    text-decoration: none;
    font-size: 0.9rem;
    font-weight: 500;
    transition: color 0.2s;
  }
  .links a:hover { color: var(--text); }

  .btn-nav {
    background: var(--accent) !important;
    color: #fff !important;
    padding: 0.45rem 1.1rem;
    border-radius: 6px;
    font-weight: 600 !important;
    transition: background 0.2s, transform 0.15s !important;
  }
  .btn-nav:hover {
    background: var(--accent-h) !important;
    transform: translateY(-1px);
  }

  /* Language picker */
  .lang-picker { position: relative; }

  .lang-btn {
    display: flex;
    align-items: center;
    gap: 0.4rem;
    background: var(--elevated);
    border: 1px solid var(--border);
    color: var(--text-dim);
    padding: 0.35rem 0.7rem;
    border-radius: 6px;
    font-size: 0.82rem;
    font-weight: 500;
    cursor: pointer;
    transition: border-color 0.2s, color 0.2s;
  }
  .lang-btn:hover { border-color: var(--accent); color: var(--text); }

  .lang-name { max-width: 70px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }

  .lang-menu {
    position: absolute;
    top: calc(100% + 6px);
    right: 0;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    overflow: hidden;
    min-width: 140px;
    box-shadow: 0 8px 32px rgba(0,0,0,0.4);
    z-index: 200;
  }
  .lang-item {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    width: 100%;
    padding: 0.5rem 0.85rem;
    background: none;
    border: none;
    color: var(--text-dim);
    font-size: 0.85rem;
    cursor: pointer;
    transition: background 0.15s, color 0.15s;
    text-align: left;
  }
  .lang-item:hover { background: var(--elevated); color: var(--text); }
  .lang-item.active { color: var(--accent); background: var(--accent-d); }

  @media (max-width: 768px) {
    .inner { padding: 0 1.25rem; }
    .lang-name { display: none; }
    .links { gap: 0.75rem; }
  }
</style>
