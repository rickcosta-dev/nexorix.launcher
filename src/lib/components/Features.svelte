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

<section id="features" bind:this={section}>
  <div class="container">
    <div class="header" class:visible>
      <span class="tag">{$t.featTag}</span>
      <h2>{$t.featTitle}<br /><span>{$t.featSub}</span></h2>
      <p>{$t.featDesc}</p>
    </div>
    <div class="grid" class:visible>
      {#each $t.features as f, i}
        <div class="card" style="--delay: {i * 50}ms">
          <div class="icon">{f.icon}</div>
          <h3>{f.title}</h3>
          <p>{f.desc}</p>
        </div>
      {/each}
    </div>
  </div>
</section>

<style>
  section { padding: 6rem 0; position: relative; z-index: 1; }
  .container { width: 100%; max-width: var(--max-w); margin: 0 auto; padding: 0 var(--pad); }
  .header { text-align: center; margin-bottom: 3.5rem; opacity: 0; transform: translateY(24px); transition: opacity 0.7s, transform 0.7s; }
  .header.visible { opacity: 1; transform: none; }
  .tag { display: inline-block; background: var(--accent-d); color: var(--accent-h); border: 1px solid rgba(124,92,255,0.25); padding: 0.3rem 0.9rem; border-radius: 100px; font-size: 0.78rem; font-weight: 600; letter-spacing: 0.05em; margin-bottom: 1rem; }
  h2 { font-size: clamp(1.8rem, 3vw, 2.6rem); font-weight: 800; line-height: 1.2; margin-bottom: 0.75rem; }
  h2 span { color: var(--accent); }
  .header p { color: var(--text-dim); font-size: 1rem; }
  .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 1.25rem; }
  .grid.visible .card { opacity: 1; transform: none; }
  .card { background: var(--surface); border: 1px solid var(--border); border-radius: 12px; padding: 1.5rem; transition: border-color 0.25s, transform 0.25s, box-shadow 0.25s, opacity 0.5s var(--delay), transform 0.5s var(--delay); opacity: 0; transform: translateY(20px); }
  .card:hover { border-color: rgba(124,92,255,0.4); transform: translateY(-4px); box-shadow: 0 8px 32px rgba(124,92,255,0.12); }
  .icon { font-size: 1.8rem; margin-bottom: 0.75rem; display: block; }
  h3 { font-size: 1rem; font-weight: 700; margin-bottom: 0.5rem; color: var(--text); }
  .card p { font-size: 0.875rem; color: var(--text-dim); line-height: 1.6; }
</style>
