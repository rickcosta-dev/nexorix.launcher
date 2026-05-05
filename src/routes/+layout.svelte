<script>
  import '../app.css';
  import { onMount } from 'svelte';

  // Load Inter font
  onMount(() => {
    const link = document.createElement('link');
    link.rel = 'stylesheet';
    link.href = 'https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap';
    document.head.appendChild(link);
  });
</script>

<slot />
