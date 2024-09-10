<script lang="ts">
  import './app.css';
  import Input from './lib/Input.svelte';
  import InfoBox from './lib/InfoBox.svelte';

  let showInfoBox = false;
  let infoBoxType: 'info' | 'warn' | 'error' = 'info';
  let infoBoxMessage = '';

  function register(event: SubmitEvent) {
    event.preventDefault();

    const formData = new FormData(event.target as HTMLFormElement);
    const data = Object.fromEntries(formData.entries());

    const name = data['name'];
    if (!name) {
      showInfoBoxMessage('error', 'Név megadása kötelező');
      return;
    }

    const email = data['email'];
    if (!email) {
      showInfoBoxMessage('error', 'Email megadása kötelező');
      return;
    }

    const password = data['password'];
    if (!password) {
      showInfoBoxMessage('error', 'Jelszó megadása kötelező');
      return;
    }

    showInfoBoxMessage('info', 'Sikeres regisztráció!');
  }

  function showInfoBoxMessage(type: 'info' | 'warn' | 'error', text: string) {
    showInfoBox = true;
    infoBoxType = type;
    infoBoxMessage = text;

    setTimeout(() => {
      showInfoBox = false;
    }, 3000);
  }
</script>

<main class="absolute w-full h-full flex justify-center items-center">
  <form
    on:submit="{register}"
    class="flex flex-col gap-2"
  >
    <div class="p-2 text-white text-4xl flex justify-center">
      <span>Regisztráció</span>
    </div>

    <Input
      type="text"
      placeholder="Add meg neved"
      name="name"
    ></Input>

    <Input
      type="email"
      placeholder="Add meg az email-ed"
      name="email"
    ></Input>

    <Input
      type="password"
      placeholder="Add meg a jelszavad"
      name="password"
    ></Input>

    <button
      class="p-2 rounded-md bg-sky-600 text-white outline-none"
      type="submit">Regisztráció</button
    >
  </form>

  {#if showInfoBox}
    <InfoBox
      type="{infoBoxType}"
      message="{infoBoxMessage}"
    ></InfoBox>
  {/if}
</main>
