<script>
  import { onMount } from 'svelte';
  import { t } from '$lib/i18n.js';
  let section, visible = false;
  onMount(() => {
    const obs = new IntersectionObserver(([e]) => { if (e.isIntersecting) visible = true; }, { threshold: 0.15 });
    obs.observe(section);
    return () => obs.disconnect();
  });
</script>

<section id="developer" bind:this={section}>
  <div class="container">
    <div class="header" class:visible>
      <span class="tag">{$t.devTag}</span>
      <h2>{$t.devTitle}<br /><span>{$t.devSub}</span></h2>
    </div>

    <div class="card" class:visible>
      <!-- Avatar with real photo -->
      <div class="avatar-wrap">
        <div class="avatar">
          <img src="/developer.png" alt="RickZIn021" />
        </div>
        <div class="avatar-ring" />
        <div class="status-badge">
          <span class="status-dot" />
          {$t.devAvail}
        </div>
      </div>

      <div class="info">
        <div class="name-row">
          <h3>RickZIn021</h3>
          <span class="role">{$t.devRole}</span>
        </div>

        <p class="bio">{@html $t.devBio}</p>

        <div class="tech-tags">
          {#each ['C++17', 'DirectX 9', 'WinAPI', 'Dear ImGui', 'SA-MP', 'Windows'] as t}
            <span class="tech-tag">{t}</span>
          {/each}
        </div>

        <div class="links">
          <a href="https://github.com/rickcosta-dev" target="_blank" rel="noopener" class="link-btn github">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/>
            </svg>
            rickcosta-dev
          </a>

          <a href="https://discord.com/users/917890301547393024" target="_blank" rel="noopener" class="link-btn discord">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
              <path d="M20.317 4.37a19.791 19.791 0 0 0-4.885-1.515.074.074 0 0 0-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 0 0-5.487 0 12.64 12.64 0 0 0-.617-1.25.077.077 0 0 0-.079-.037A19.736 19.736 0 0 0 3.677 4.37a.07.07 0 0 0-.032.027C.533 9.046-.32 13.58.099 18.057a.082.082 0 0 0 .031.057 19.9 19.9 0 0 0 5.993 3.03.078.078 0 0 0 .084-.028c.462-.63.874-1.295 1.226-1.994a.076.076 0 0 0-.041-.106 13.107 13.107 0 0 1-1.872-.892.077.077 0 0 1-.008-.128 10.2 10.2 0 0 0 .372-.292.074.074 0 0 1 .077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 0 1 .078.01c.12.098.246.198.373.292a.077.077 0 0 1-.006.127 12.299 12.299 0 0 1-1.873.892.077.077 0 0 0-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 0 0 .084.028 19.839 19.839 0 0 0 6.002-3.03.077.077 0 0 0 .032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 0 0-.031-.03zM8.02 15.33c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.956-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.956 2.418-2.157 2.418zm7.975 0c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.955-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.946 2.418-2.157 2.418z"/>
            </svg>
            rickzin021
          </a>

          <div class="discord-id">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor" style="opacity:0.5">
              <path d="M20.317 4.37a19.791 19.791 0 0 0-4.885-1.515.074.074 0 0 0-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 0 0-5.487 0 12.64 12.64 0 0 0-.617-1.25.077.077 0 0 0-.079-.037A19.736 19.736 0 0 0 3.677 4.37a.07.07 0 0 0-.032.027C.533 9.046-.32 13.58.099 18.057a.082.082 0 0 0 .031.057 19.9 19.9 0 0 0 5.993 3.03.078.078 0 0 0 .084-.028c.462-.63.874-1.295 1.226-1.994a.076.076 0 0 0-.041-.106 13.107 13.107 0 0 1-1.872-.892.077.077 0 0 1-.008-.128 10.2 10.2 0 0 0 .372-.292.074.074 0 0 1 .077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 0 1 .078.01c.12.098.246.198.373.292a.077.077 0 0 1-.006.127 12.299 12.299 0 0 1-1.873.892.077.077 0 0 0-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 0 0 .084.028 19.839 19.839 0 0 0 6.002-3.03.077.077 0 0 0 .032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 0 0-.031-.03z"/>
            </svg>
            ID: 917890301547393024
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  section {
    padding: 6rem 2rem;
    position: relative;
    z-index: 1;
  }
  .container { max-width: 900px; margin: 0 auto; }

  .header {
    text-align: center;
    margin-bottom: 3rem;
    opacity: 0; transform: translateY(24px);
    transition: opacity 0.7s, transform 0.7s;
  }
  .header.visible { opacity: 1; transform: none; }

  .tag {
    display: inline-block;
    background: var(--accent-d);
    color: var(--accent-h);
    border: 1px solid rgba(124,92,255,0.25);
    padding: 0.3rem 0.9rem;
    border-radius: 100px;
    font-size: 0.78rem;
    font-weight: 600;
    letter-spacing: 0.05em;
    margin-bottom: 1rem;
  }
  h2 { font-size: clamp(1.8rem, 3vw, 2.6rem); font-weight: 800; line-height: 1.2; margin-bottom: 0.75rem; }
  h2 span { color: var(--accent); }

  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 2.5rem;
    display: flex;
    gap: 2.5rem;
    align-items: flex-start;
    opacity: 0; transform: translateY(24px);
    transition: opacity 0.7s 0.2s, transform 0.7s 0.2s;
    position: relative;
    overflow: hidden;
  }
  .card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, var(--accent), transparent);
  }
  .card.visible { opacity: 1; transform: none; }

  /* Avatar */
  .avatar-wrap {
    position: relative;
    flex-shrink: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.75rem;
  }
  .avatar {
    width: 96px; height: 96px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--accent), #a855f7);
    display: flex; align-items: center; justify-content: center;
    font-size: 2.5rem;
    font-weight: 900;
    color: #fff;
    position: relative;
    z-index: 1;
    overflow: hidden;
  }
  .avatar img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 50%;
    display: block;
  }
  .avatar-ring {
    position: absolute;
    top: -4px; left: -4px;
    width: 104px; height: 104px;
    border-radius: 50%;
    border: 2px solid var(--accent);
    opacity: 0.4;
    animation: spin 8s linear infinite;
  }
  @keyframes spin { to { transform: rotate(360deg); } }

  .status-badge {
    display: flex;
    align-items: center;
    gap: 0.35rem;
    background: rgba(56,201,107,0.12);
    border: 1px solid rgba(56,201,107,0.25);
    color: #38c96b;
    padding: 0.2rem 0.6rem;
    border-radius: 100px;
    font-size: 0.7rem;
    font-weight: 600;
    white-space: nowrap;
  }
  .status-dot {
    width: 6px; height: 6px;
    border-radius: 50%;
    background: #38c96b;
    animation: pulse 2s infinite;
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.4; }
  }

  /* Info */
  .info { flex: 1; min-width: 0; }

  .name-row { margin-bottom: 0.75rem; }
  h3 {
    font-size: 1.6rem;
    font-weight: 800;
    color: var(--text);
    margin-bottom: 0.2rem;
  }
  .role {
    font-size: 0.85rem;
    color: var(--accent);
    font-weight: 500;
  }

  .bio { color: var(--text-dim); font-size: 0.95rem; line-height: 1.7; margin-bottom: 1.25rem; }
  .bio :global(strong) { color: var(--text); }

  .tech-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-bottom: 1.5rem;
  }
  .tech-tag {
    background: var(--elevated);
    border: 1px solid var(--border);
    color: var(--text-dim);
    padding: 0.2rem 0.65rem;
    border-radius: 6px;
    font-size: 0.75rem;
    font-weight: 600;
    font-family: 'Courier New', monospace;
  }

  .links {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
    align-items: center;
  }

  .link-btn {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.55rem 1.1rem;
    border-radius: 8px;
    font-size: 0.875rem;
    font-weight: 600;
    text-decoration: none;
    transition: transform 0.15s, box-shadow 0.2s;
  }
  .link-btn:hover { transform: translateY(-2px); }

  .github {
    background: #24292e;
    color: #fff;
    border: 1px solid #444;
  }
  .github:hover { box-shadow: 0 4px 16px rgba(0,0,0,0.4); }

  .discord {
    background: #5865f2;
    color: #fff;
  }
  .discord:hover { box-shadow: 0 4px 16px rgba(88,101,242,0.4); }

  .discord-id {
    display: flex;
    align-items: center;
    gap: 0.35rem;
    font-size: 0.75rem;
    color: var(--text-muted);
    font-family: 'Courier New', monospace;
  }

  @media (max-width: 640px) {
    .card { flex-direction: column; align-items: center; text-align: center; }
    .tech-tags, .links { justify-content: center; }
  }
</style>
