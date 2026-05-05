<script>
  import { onMount } from 'svelte';
  import { t } from '$lib/i18n.js';
  let section, visible = false;
  onMount(() => {
    const obs = new IntersectionObserver(([e]) => { if (e.isIntersecting) visible = true; }, { threshold: 0.1 });
    obs.observe(section);
    return () => obs.disconnect();
  });
</script>

<section id="tech" bind:this={section}>
  <div class="container">
    <div class="header" class:visible>
      <span class="tag">{$t.techTag}</span>
      <h2>{$t.techTitle}<br /><span>{$t.techSub}</span></h2>
      <p>{$t.techDesc}</p>
    </div>
    <div class="grid" class:visible>
      {#each $t.stack as item, i}
        <div class="card" style="--delay: {i * 50}ms; --c: {item.color}">
          <div class="pill" style="background: {item.color}20; color: {item.color}; border-color: {item.color}40">{item.name}</div>
          <p>{item.desc}</p>
        </div>
      {/each}
    </div>
  </div>
</section>

<style>
  section { padding: 6rem 0; background: linear-gradient(180deg, transparent, rgba(124,92,255,0.03), transparent); position: relative; z-index: 1; }
  .container { width: 100%; max-width: var(--max-w); margin: 0 auto; padding: 0 var(--pad); }
  .header { text-align: center; margin-bottom: 3rem; opacity: 0; transform: translateY(24px); transition: opacity 0.7s, transform 0.7s; }
  .header.visible { opacity: 1; transform: none; }
  .tag { display: inline-block; background: var(--accent-d); color: var(--accent-h); border: 1px solid rgba(124,92,255,0.25); padding: 0.3rem 0.9rem; border-radius: 100px; font-size: 0.78rem; font-weight: 600; letter-spacing: 0.05em; margin-bottom: 1rem; }
  h2 { font-size: clamp(1.8rem, 3vw, 2.6rem); font-weight: 800; line-height: 1.2; margin-bottom: 0.75rem; }
  h2 span { color: var(--accent); }
  .header p { color: var(--text-dim); }
  .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(240px, 1fr)); gap: 1rem; }
  .grid.visible .card { opacity: 1; transform: none; }
  .card { background: var(--surface); border: 1px solid var(--border); border-radius: 10px; padding: 1.25rem; opacity: 0; transform: translateY(16px); transition: opacity 0.5s var(--delay), transform 0.5s var(--delay), border-color 0.2s; }
  .card:hover { border-color: var(--c, var(--accent)); }
  .pill { display: inline-block; padding: 0.25rem 0.75rem; border-radius: 100px; font-size: 0.8rem; font-weight: 700; border: 1px solid; margin-bottom: 0.6rem; }
  .card p { font-size: 0.82rem; color: var(--text-dim); line-height: 1.5; }
</style>
