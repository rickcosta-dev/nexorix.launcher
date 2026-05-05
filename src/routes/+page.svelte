<script>
  import { onMount } from 'svelte';
  import Hero from '$lib/components/Hero.svelte';
  import Features from '$lib/components/Features.svelte';
  import TechStack from '$lib/components/TechStack.svelte';
  import Screenshots from '$lib/components/Screenshots.svelte';
  import Developer from '$lib/components/Developer.svelte';
  import Download from '$lib/components/Download.svelte';
  import Navbar from '$lib/components/Navbar.svelte';
  import Footer from '$lib/components/Footer.svelte';
  import ParticlesBg from '$lib/components/ParticlesBg.svelte';

  let mounted = false;
  onMount(() => { mounted = true; });
</script>

<svelte:head>
  <title>NEXORIX Launcher — SA-MP</title>
</svelte:head>

<ParticlesBg />
<Navbar />

<main>
  <Hero />
  <Features />
  <TechStack />
  <Screenshots />
  <Developer />
  <Download />
</main>

<Footer />

<style>
  main {
    position: relative;
    z-index: 1;
  }
</style>
