<script>
  import { onMount } from 'svelte';
  import { t } from '$lib/i18n.js';

  let section, visible = false;
  let active = 0;

  onMount(() => {
    const obs = new IntersectionObserver(([e]) => { if (e.isIntersecting) visible = true; }, { threshold: 0.1 });
    obs.observe(section);
    const interval = setInterval(() => { active = (active + 1) % 3; }, 3000);
    return () => { obs.disconnect(); clearInterval(interval); };
  });
</script>

<section bind:this={section}>
  <div class="container">
    <div class="header" class:visible>
      <span class="tag">{$t.screensTag}</span>
      <h2>{$t.screensTitle}<br /><span>{$t.screensSub}</span></h2>
      <p>{$t.screensDesc}</p>
    </div>

    <div class="showcase" class:visible>
      <!-- Fake window preview -->
      <div class="window">
        <div class="win-bar">
          <div class="win-dots">
            <span style="background:#f44" />
            <span style="background:#fa0" />
            <span style="background:#4c4" />
          </div>
          <span class="win-title">NEXORIX LAUNCHER — {$t.screenTabs[active].title}</span>
        </div>

        <div class="win-body">
          <!-- Sidebar -->
          <div class="sidebar">
            <div class="s-logo"><span style="color:var(--accent);font-weight:900">N</span>EXORIX</div>
            <div class="s-section">{$t.tabInternet?.toUpperCase() ?? 'NAVEGAÇÃO'}</div>
            {#each [$t.tabInternet, $t.tabFav, $t.tabHistory] as item, i}
              <div class="s-item" class:active={i === 0}>{item}</div>
            {/each}
          </div>

          <!-- Main content -->
          <div class="main">
            <div class="toolbar">
              <div class="search-box">🔍 {$t.searchHint}</div>
              <div class="toolbar-right">
                <span class="t-count">5 {$t.serverCount}</span>
                <button class="t-btn accent">↻</button>
                <button class="t-btn">+</button>
              </div>
            </div>

            <div class="col-headers">
              <span>{$t.serverCol?.toUpperCase()}</span>
              <span>{$t.players?.toUpperCase()}</span>
              <span>{$t.ping?.toUpperCase()}</span>
              <span>{$t.actionCol?.toUpperCase()}</span>
            </div>

            {#each [
              { name: 'Brasil RP — Servidor Oficial', gm: 'Roleplay', p: '312/500', ping: 42 },
              { name: 'Roleplay Brasil — Vida Real',  gm: 'Roleplay', p: '198/300', ping: 67 },
              { name: 'Freeroam BR — Sem Regras',     gm: 'Freeroam', p: '89/200',  ping: 31 },
              { name: 'DM Server — Deathmatch',       gm: 'Deathmatch',p: '45/100', ping: 88 },
              { name: 'Cops and Robbers BR',           gm: 'C&R',      p: '12/150', ping: 120 },
            ] as row, i}
              <div class="row" class:selected={i === 1}>
                <div class="row-name">
                  <span class="online-dot" />
                  <div>
                    <div class="rn">{row.name}</div>
                    <div class="rgm">{row.gm}</div>
                  </div>
                </div>
                <span class="rp" style="color:{parseInt(row.p) > 200 ? '#f87' : '#38c96b'}">{row.p}</span>
                <span class="rping" style="color:{row.ping < 80 ? '#38c96b' : row.ping < 150 ? '#fa0' : '#f44'}">{row.ping}ms</span>
                <button class="connect-btn">{$t.connectBtn}</button>
              </div>
            {/each}
          </div>
        </div>
      </div>

      <!-- Tabs -->
      <div class="tabs">
        {#each $t.screenTabs as s, i}
          <button class="tab" class:active={active === i} on:click={() => active = i}
                  style="--tc: {['#7c5cff','#38c96b','#fa8c16'][i]}">
            <span class="tab-dot" style="background:{['#7c5cff','#38c96b','#fa8c16'][i]}" />
            <div>
              <div class="tab-title">{s.title}</div>
              <div class="tab-desc">{s.desc}</div>
            </div>
          </button>
        {/each}
      </div>
    </div>
  </div>
</section>

<style>
  section { padding: 6rem 0; position: relative; z-index: 1; }
  .container { width: 100%; max-width: var(--max-w); margin: 0 auto; padding: 0 var(--pad); }
  .header { text-align: center; margin-bottom: 3rem; opacity: 0; transform: translateY(24px); transition: opacity 0.7s, transform 0.7s; }
  .header.visible { opacity: 1; transform: none; }
  .tag { display: inline-block; background: var(--accent-d); color: var(--accent-h); border: 1px solid rgba(124,92,255,0.25); padding: 0.3rem 0.9rem; border-radius: 100px; font-size: 0.78rem; font-weight: 600; letter-spacing: 0.05em; margin-bottom: 1rem; }
  h2 { font-size: clamp(1.8rem, 3vw, 2.6rem); font-weight: 800; line-height: 1.2; margin-bottom: 0.75rem; }
  h2 span { color: var(--accent); }
  .header p { color: var(--text-dim); }
  .showcase { display: flex; gap: 2rem; align-items: flex-start; opacity: 0; transform: translateY(24px); transition: opacity 0.7s 0.2s, transform 0.7s 0.2s; }
  .showcase.visible { opacity: 1; transform: none; }

  .window { flex: 1; background: var(--surface); border: 1px solid var(--border); border-radius: 12px; overflow: hidden; box-shadow: 0 24px 80px rgba(0,0,0,0.5); min-width: 0; }
  .win-bar { background: var(--elevated); padding: 0.55rem 1rem; display: flex; align-items: center; gap: 0.75rem; border-bottom: 1px solid var(--border); }
  .win-dots { display: flex; gap: 5px; }
  .win-dots span { width: 9px; height: 9px; border-radius: 50%; }
  .win-title { font-size: 0.7rem; font-weight: 700; letter-spacing: 0.08em; color: var(--text-muted); flex: 1; text-align: center; }
  .win-body { display: flex; height: 340px; }

  .sidebar { width: 140px; background: var(--elevated); border-right: 1px solid var(--border); padding: 0.75rem 0; flex-shrink: 0; }
  .s-logo { font-size: 0.85rem; font-weight: 800; letter-spacing: 0.05em; padding: 0 0.75rem 0.75rem; border-bottom: 1px solid var(--border); margin-bottom: 0.5rem; }
  .s-section { font-size: 0.6rem; font-weight: 700; color: var(--text-muted); letter-spacing: 0.1em; padding: 0.4rem 0.75rem 0.2rem; }
  .s-item { padding: 0.4rem 0.75rem; font-size: 0.75rem; color: var(--text-dim); cursor: default; border-left: 2px solid transparent; }
  .s-item.active { color: var(--accent); border-color: var(--accent); background: var(--accent-d); }

  .main { flex: 1; display: flex; flex-direction: column; overflow: hidden; }
  .toolbar { display: flex; align-items: center; gap: 0.5rem; padding: 0.4rem 0.6rem; border-bottom: 1px solid var(--border); background: var(--bg); }
  .search-box { flex: 1; background: var(--elevated); border-radius: 5px; padding: 0.25rem 0.6rem; font-size: 0.7rem; color: var(--text-muted); }
  .toolbar-right { display: flex; align-items: center; gap: 4px; }
  .t-count { font-size: 0.65rem; color: var(--text-muted); margin-right: 4px; }
  .t-btn { width: 24px; height: 24px; background: var(--elevated); border: none; border-radius: 4px; color: var(--text-dim); font-size: 0.7rem; cursor: default; display: flex; align-items: center; justify-content: center; }
  .t-btn.accent { background: var(--accent); color: #fff; }
  .col-headers { display: grid; grid-template-columns: 1fr 70px 55px 70px; padding: 0.3rem 0.6rem; font-size: 0.62rem; font-weight: 700; color: var(--text-muted); letter-spacing: 0.06em; background: var(--elevated); border-bottom: 1px solid var(--border); }
  .row { display: grid; grid-template-columns: 1fr 70px 55px 70px; align-items: center; padding: 0.4rem 0.6rem; border-bottom: 1px solid rgba(255,255,255,0.03); }
  .row.selected { background: rgba(124,92,255,0.08); }
  .row-name { display: flex; align-items: center; gap: 0.4rem; min-width: 0; }
  .online-dot { width: 6px; height: 6px; border-radius: 50%; background: #38c96b; flex-shrink: 0; }
  .rn { font-size: 0.72rem; color: var(--text); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
  .rgm { font-size: 0.62rem; color: var(--text-muted); }
  .rp, .rping { font-size: 0.7rem; font-weight: 600; }
  .connect-btn { background: var(--accent); color: #fff; border: none; border-radius: 4px; padding: 0.18rem 0.45rem; font-size: 0.65rem; font-weight: 600; cursor: default; }

  .tabs { display: flex; flex-direction: column; gap: 0.75rem; width: 260px; flex-shrink: 0; }
  .tab { display: flex; align-items: flex-start; gap: 0.75rem; background: var(--surface); border: 1px solid var(--border); border-radius: 10px; padding: 1rem; cursor: pointer; text-align: left; transition: border-color 0.2s, background 0.2s; }
  .tab.active { border-color: var(--tc); background: color-mix(in srgb, var(--tc) 8%, var(--surface)); }
  .tab-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; margin-top: 4px; }
  .tab-title { font-size: 0.85rem; font-weight: 700; color: var(--text); margin-bottom: 0.25rem; }
  .tab-desc { font-size: 0.75rem; color: var(--text-dim); line-height: 1.4; }

  @media (max-width: 900px) {
    .showcase { flex-direction: column; }
    .tabs { width: 100%; flex-direction: row; flex-wrap: wrap; }
    .tab { flex: 1; min-width: 200px; }
  }
</style>
