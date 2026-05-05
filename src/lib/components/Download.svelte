<script>
  import { onMount } from 'svelte';
  import { t } from '$lib/i18n.js';
  let section, visible = false, downloading = false;

  // Google Drive direct download link
  const DOWNLOAD_URL = 'https://drive.google.com/uc?export=download&id=1xyfhedAwmrRCoy3vL895HuWnCJ7mpnyk';
  const GDRIVE_VIEW  = 'https://drive.google.com/file/d/1xyfhedAwmrRCoy3vL895HuWnCJ7mpnyk/view?usp=sharing';

  function handleDownload() {
    downloading = true;
    // Open download in new tab
    window.open(DOWNLOAD_URL, '_blank');
    setTimeout(() => { downloading = false; }, 3000);
  }

  onMount(() => {
    const obs = new IntersectionObserver(([e]) => { if (e.isIntersecting) visible = true; }, { threshold: 0.15 });
    obs.observe(section);
    return () => obs.disconnect();
  });
</script>

<section id="download" bind:this={section}>
  <div class="bg-glow" />
  <div class="container">
    <div class="content" class:visible>
      <span class="tag">{$t.dlTag}</span>
      <h2>{$t.dlTitle}<br /><span>{$t.dlSub}</span></h2>
      <p>{$t.dlDesc}</p>

      <div class="download-box">
        <div class="version-info">
          <div class="v-badge">v1.0.0</div>
          <div class="v-details">
            <span class="v-name">NexorixLauncher.exe</span>
            <span class="v-meta">Windows x64 · ~5 MB</span>
          </div>
        </div>

        <button class="btn-download" class:loading={downloading} on:click={handleDownload}>
          {#if downloading}
            <span class="spinner" />
            {$t.dlLoading}
          {:else}
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
              <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/>
              <polyline points="7 10 12 15 17 10"/>
              <line x1="12" y1="15" x2="12" y2="3"/>
            </svg>
            {$t.dlFree}
          {/if}
        </button>

        <!-- Fallback link -->
        <a href={GDRIVE_VIEW} target="_blank" rel="noopener" class="gdrive-link">
          <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor">
            <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-1 14H9V8h2v8zm4 0h-2V8h2v8z"/>
          </svg>
          {$t.openGDrive}
        </a>
      </div>

      <!-- Requirements -->
      <div class="requirements">
        {#each $t.requirements as r}
          <div class="req">
            <span class="req-icon">{r.icon}</span>
            <div class="req-label">{r.label}</div>
            <div class="req-sub">{r.sub}</div>
          </div>
        {/each}
      </div>

      <!-- Steps -->
      <div class="steps">
        <div class="steps-title">{$t.reqTitle}</div>
        <div class="steps-list">
          {#each $t.steps as step, i}
            <div class="step">
              <span class="step-num">{i + 1}</span>
              <span>{step}</span>
            </div>
          {/each}
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  section { padding: 6rem 0 8rem; position: relative; z-index: 1; overflow: hidden; }
  .bg-glow { position: absolute; top: 50%; left: 50%; transform: translate(-50%,-50%); width: 600px; height: 400px; background: radial-gradient(ellipse, rgba(124,92,255,0.12) 0%, transparent 70%); pointer-events: none; }
  .container { width: 100%; max-width: 700px; margin: 0 auto; padding: 0 var(--pad); }
  .content { text-align: center; opacity: 0; transform: translateY(24px); transition: opacity 0.7s, transform 0.7s; }
  .content.visible { opacity: 1; transform: none; }
  .tag { display: inline-block; background: var(--accent-d); color: var(--accent-h); border: 1px solid rgba(124,92,255,0.25); padding: 0.3rem 0.9rem; border-radius: 100px; font-size: 0.78rem; font-weight: 600; letter-spacing: 0.05em; margin-bottom: 1rem; }
  h2 { font-size: clamp(2rem, 4vw, 3rem); font-weight: 900; line-height: 1.1; margin-bottom: 0.75rem; }
  h2 span { color: var(--accent); }
  .content > p { color: var(--text-dim); margin-bottom: 2.5rem; font-size: 1rem; }
  .download-box { background: var(--surface); border: 1px solid var(--border); border-radius: 16px; padding: 1.75rem; margin-bottom: 2rem; display: flex; flex-direction: column; align-items: center; gap: 1rem; }
  .version-info { display: flex; align-items: center; gap: 1rem; width: 100%; }
  .v-badge { background: var(--accent-d); color: var(--accent); border: 1px solid rgba(124,92,255,0.3); padding: 0.3rem 0.75rem; border-radius: 6px; font-size: 0.8rem; font-weight: 700; font-family: monospace; white-space: nowrap; }
  .v-details { text-align: left; }
  .v-name { display: block; font-weight: 700; font-size: 0.95rem; }
  .v-meta { display: block; font-size: 0.75rem; color: var(--text-muted); }
  .btn-download { width: 100%; display: flex; align-items: center; justify-content: center; gap: 0.6rem; background: var(--accent); color: #fff; border: none; border-radius: 10px; padding: 0.9rem 2rem; font-size: 1rem; font-weight: 700; cursor: pointer; transition: background 0.2s, transform 0.15s, box-shadow 0.2s; box-shadow: 0 4px 24px rgba(124,92,255,0.4); }
  .btn-download:hover:not(.loading) { background: var(--accent-h); transform: translateY(-2px); box-shadow: 0 8px 32px rgba(124,92,255,0.55); }
  .btn-download.loading { opacity: 0.7; cursor: not-allowed; }
  .spinner { width: 18px; height: 18px; border: 2px solid rgba(255,255,255,0.3); border-top-color: #fff; border-radius: 50%; animation: spin 0.7s linear infinite; }
  @keyframes spin { to { transform: rotate(360deg); } }

  .gdrive-link {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    color: var(--text-muted);
    font-size: 0.8rem;
    text-decoration: none;
    transition: color 0.2s;
    padding: 0.25rem 0;
  }
  .gdrive-link:hover { color: var(--text-dim); }
  .requirements { display: grid; grid-template-columns: repeat(4, 1fr); gap: 1rem; margin-bottom: 2rem; }
  .req { background: var(--surface); border: 1px solid var(--border); border-radius: 10px; padding: 1rem 0.75rem; display: flex; flex-direction: column; align-items: center; gap: 0.4rem; text-align: center; }
  .req-icon { font-size: 1.4rem; }
  .req-label { font-size: 0.8rem; font-weight: 700; color: var(--text); }
  .req-sub { font-size: 0.7rem; color: var(--text-muted); }
  .steps { background: var(--surface); border: 1px solid var(--border); border-radius: 12px; padding: 1.5rem; text-align: left; }
  .steps-title { font-size: 0.8rem; font-weight: 700; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.08em; margin-bottom: 1rem; }
  .steps-list { display: flex; flex-direction: column; gap: 0.6rem; }
  .step { display: flex; align-items: center; gap: 0.75rem; font-size: 0.875rem; color: var(--text-dim); }
  .step-num { width: 22px; height: 22px; background: var(--accent-d); color: var(--accent); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 0.7rem; font-weight: 700; flex-shrink: 0; }
  @media (max-width: 600px) { .requirements { grid-template-columns: repeat(2, 1fr); } }
</style>
