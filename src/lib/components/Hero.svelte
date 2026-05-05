<script>
  import { onMount } from 'svelte';
  import { fly, fade } from 'svelte/transition';
  import { t } from '$lib/i18n.js';

  let visible = false;
  onMount(() => { setTimeout(() => visible = true, 100); });
</script>

<section class="hero">
  <div class="orb orb1" />
  <div class="orb orb2" />

  {#if visible}
    <div class="inner">
      <div class="content">
        <div class="badge" in:fly={{ y: -20, duration: 600, delay: 100 }}>
          <span class="dot" />
          {$t.badge}
        </div>

        <h1 in:fly={{ y: 30, duration: 700, delay: 200 }}>
          <span class="accent">NEXORIX</span><br />
          {$t.heroTitle}
        </h1>

        <p class="subtitle" in:fly={{ y: 20, duration: 700, delay: 350 }}>
          {@html $t.heroSub}
        </p>

        <div class="cta-row" in:fly={{ y: 20, duration: 700, delay: 500 }}>
          <a href="#download" class="btn-primary">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
              <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/>
              <polyline points="7 10 12 15 17 10"/>
              <line x1="12" y1="15" x2="12" y2="3"/>
            </svg>
            {$t.dlBtn}
          </a>
        </div>

        <div class="stats" in:fade={{ duration: 800, delay: 700 }}>
          <div class="stat"><span class="stat-val">C++17</span><span class="stat-label">{$t.statLang}</span></div>
          <div class="divider" />
          <div class="stat"><span class="stat-val">DirectX 9</span><span class="stat-label">{$t.statRender}</span></div>
          <div class="divider" />
          <div class="stat"><span class="stat-val">Dear ImGui</span><span class="stat-label">{$t.statUI}</span></div>
          <div class="divider" />
          <div class="stat"><span class="stat-val">SA-MP</span><span class="stat-label">{$t.statPlat}</span></div>
        </div>
      </div>

      <div class="mockup-wrap" in:fly={{ x: 60, duration: 900, delay: 400 }}>
        <div class="mockup">
          <div class="mockup-bar">
            <div class="mockup-dots">
              <span style="background:#f44" />
              <span style="background:#fa0" />
              <span style="background:#4c4" />
            </div>
            <span class="mockup-title">NEXORIX LAUNCHER</span>
          </div>
          <div class="mockup-body">
            <div class="m-tabs">
              <span class="m-tab active">{$t.tabInternet}</span>
              <span class="m-tab">{$t.tabFav}</span>
              <span class="m-tab">{$t.tabHistory}</span>
            </div>
            <div class="m-toolbar">
              <div class="m-search">🔍 {$t.searchHint}</div>
              <div class="m-btns">
                <span class="m-btn accent">↻</span>
                <span class="m-btn">▶</span>
                <span class="m-btn">+</span>
              </div>
            </div>
            <div class="m-rows">
              {#each [
                { name: 'Brasil RP — Servidor Oficial', players: '312/500', ping: 42 },
                { name: 'Roleplay Brasil — Vida Real',  players: '198/300', ping: 67 },
                { name: 'Freeroam BR — Sem Regras',     players: '89/200',  ping: 31 },
                { name: 'DM Server — Deathmatch',       players: '45/100',  ping: 88 },
                { name: 'Cops and Robbers BR',           players: '12/150',  ping: 120 },
              ] as s, i}
                <div class="m-row" style="animation-delay: {i * 80}ms">
                  <span class="m-dot" style="background: {i < 4 ? '#38c96b' : '#666'}" />
                  <span class="m-name">{s.name}</span>
                  <span class="m-players" style="color:{parseInt(s.players) > 200 ? '#f87' : '#38c96b'}">{s.players}</span>
                  <span class="m-ping" style="color:{s.ping < 80 ? '#38c96b' : s.ping < 150 ? '#fa0' : '#f44'}">{s.ping}ms</span>
                  <button class="m-connect">{$t.connectBtn}</button>
                </div>
              {/each}
            </div>
          </div>
        </div>
        <div class="mockup-glow" />
      </div>
    </div>
  {/if}
</section>

<style>
  .hero {
    min-height: 100vh;
    position: relative;
    overflow: hidden;
    display: flex;
    align-items: center;
  }
  .inner {
    width: 100%;
    max-width: var(--max-w);
    margin: 0 auto;
    padding: 8rem var(--pad) 4rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 3rem;
  }
  .orb {
    position: absolute;
    border-radius: 50%;
    filter: blur(80px);
    pointer-events: none;
    z-index: 0;
  }
  .orb1 { width: 600px; height: 600px; background: rgba(124,92,255,0.1); top: -150px; left: -100px; }
  .orb2 { width: 400px; height: 400px; background: rgba(124,92,255,0.07); bottom: 0; right: 100px; }

  .content { flex: 1; max-width: 520px; position: relative; z-index: 1; }

  .badge {
    display: inline-flex; align-items: center; gap: 0.5rem;
    background: var(--accent-d); border: 1px solid rgba(124,92,255,0.3);
    color: var(--accent-h); padding: 0.35rem 0.9rem; border-radius: 100px;
    font-size: 0.78rem; font-weight: 600; letter-spacing: 0.03em; margin-bottom: 1.5rem;
  }
  .dot { width: 7px; height: 7px; background: var(--green); border-radius: 50%; animation: pulse 2s infinite; }
  @keyframes pulse { 0%,100%{opacity:1;transform:scale(1)} 50%{opacity:.5;transform:scale(.8)} }

  h1 { font-size: clamp(2.8rem, 5vw, 4.5rem); font-weight: 900; line-height: 1.05; letter-spacing: -0.02em; margin-bottom: 1.2rem; }
  .accent { color: var(--accent); }

  .subtitle { color: var(--text-dim); font-size: 1.05rem; line-height: 1.7; margin-bottom: 2rem; }

  .cta-row { display: flex; gap: 1rem; flex-wrap: wrap; margin-bottom: 3rem; }

  .btn-primary {
    display: inline-flex; align-items: center; gap: 0.5rem;
    background: var(--accent); color: #fff; padding: 0.75rem 1.6rem;
    border-radius: 8px; font-weight: 700; font-size: 0.95rem; text-decoration: none;
    transition: background 0.2s, transform 0.15s, box-shadow 0.2s;
    box-shadow: 0 4px 24px rgba(124,92,255,0.35);
  }
  .btn-primary:hover { background: var(--accent-h); transform: translateY(-2px); box-shadow: 0 8px 32px rgba(124,92,255,0.5); }

  .stats { display: flex; align-items: center; gap: 1.5rem; flex-wrap: wrap; }
  .stat { text-align: center; }
  .stat-val { display: block; font-size: 1rem; font-weight: 700; color: var(--accent); }
  .stat-label { display: block; font-size: 0.72rem; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.06em; margin-top: 2px; }
  .divider { width: 1px; height: 32px; background: var(--border); }

  .mockup-wrap { flex: 1; max-width: 600px; position: relative; z-index: 1; }
  .mockup { background: var(--surface); border: 1px solid var(--border); border-radius: 12px; overflow: hidden; box-shadow: 0 24px 80px rgba(0,0,0,0.6), 0 0 0 1px rgba(124,92,255,0.1); }
  .mockup-bar { background: var(--elevated); padding: 0.6rem 1rem; display: flex; align-items: center; gap: 0.75rem; border-bottom: 1px solid var(--border); }
  .mockup-dots { display: flex; gap: 6px; }
  .mockup-dots span { width: 10px; height: 10px; border-radius: 50%; }
  .mockup-title { font-size: 0.72rem; font-weight: 700; letter-spacing: 0.1em; color: var(--text-muted); flex: 1; text-align: center; }
  .m-tabs { display: flex; border-bottom: 1px solid var(--border); background: var(--surface); }
  .m-tab { padding: 0.5rem 1rem; font-size: 0.78rem; color: var(--text-muted); border-bottom: 2px solid transparent; }
  .m-tab.active { color: var(--accent); border-color: var(--accent); }
  .m-toolbar { display: flex; align-items: center; gap: 0.5rem; padding: 0.5rem 0.75rem; background: var(--bg); border-bottom: 1px solid var(--border); }
  .m-search { flex: 1; background: var(--elevated); border-radius: 6px; padding: 0.3rem 0.7rem; font-size: 0.75rem; color: var(--text-muted); }
  .m-btns { display: flex; gap: 4px; }
  .m-btn { width: 28px; height: 28px; background: var(--elevated); border-radius: 5px; display: flex; align-items: center; justify-content: center; font-size: 0.75rem; color: var(--text-dim); cursor: default; }
  .m-btn.accent { background: var(--accent); color: #fff; }
  .m-rows { padding: 0.25rem 0; }
  .m-row { display: flex; align-items: center; gap: 0.5rem; padding: 0.45rem 0.75rem; font-size: 0.75rem; border-bottom: 1px solid rgba(255,255,255,0.03); animation: rowIn 0.4s ease both; }
  @keyframes rowIn { from{opacity:0;transform:translateX(-8px)} to{opacity:1;transform:translateX(0)} }
  .m-dot { width: 7px; height: 7px; border-radius: 50%; flex-shrink: 0; }
  .m-name { flex: 1; color: var(--text); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
  .m-players { font-size: 0.7rem; font-weight: 600; min-width: 52px; text-align: right; }
  .m-ping { font-size: 0.7rem; min-width: 38px; text-align: right; }
  .m-connect { background: var(--accent); color: #fff; border: none; border-radius: 4px; padding: 0.2rem 0.55rem; font-size: 0.68rem; font-weight: 600; cursor: default; white-space: nowrap; }
  .mockup-glow { position: absolute; bottom: -40px; left: 50%; transform: translateX(-50%); width: 80%; height: 80px; background: rgba(124,92,255,0.2); filter: blur(40px); border-radius: 50%; pointer-events: none; }

  @media (max-width: 960px) {
    .inner { flex-direction: column; padding-top: 6rem; }
    .mockup-wrap { max-width: 100%; width: 100%; }
  }
</style>
