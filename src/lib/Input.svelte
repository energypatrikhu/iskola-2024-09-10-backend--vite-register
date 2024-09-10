<script lang="ts">
  export let type = 'text';
  export let placeholder = '';
  export let value = '';
  export let name: string;
</script>

<label>
  {#if type === 'email'}
    <input
      type="email"
      {name}
      {placeholder}
      bind:value
    />
  {:else if type === 'password'}
    <input
      type="password"
      {name}
      {placeholder}
      bind:value
    />
  {:else}
    <input
      type="text"
      {name}
      {placeholder}
      bind:value
    />
  {/if}
</label>

<style>
  input {
    @apply p-2 rounded-md w-64 bg-neutral-600 border border-neutral-500 text-white outline-none;
  }
</style>
