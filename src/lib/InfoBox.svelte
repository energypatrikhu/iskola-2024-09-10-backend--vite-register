<script lang="ts">
  import { fly } from 'svelte/transition';

  export let message = '';
  export let type: 'info' | 'warn' | 'error' = 'info';

  $: color = type === 'info' ? 'bg-blue-500' : type === 'warn' ? 'bg-yellow-500' : 'bg-red-500';
  $: borderColor = type === 'info' ? 'border-blue-700' : type === 'warn' ? 'border-yellow-700' : 'border-red-700';
  $: textPrefix = type === 'info' ? 'Infó' : type === 'warn' ? 'Figyelem:' : 'Hiba:';
</script>

<div
  transition:fly="{{ y: -100, duration: 500 }}"
  class="absolute text-white text-center items-center text-xl flex justify-center top-0 m-8 {color} py-2 px-4 rounded-md border {borderColor}"
>
  <span><span class="font-bold">{textPrefix}</span> {message}</span>
</div>
