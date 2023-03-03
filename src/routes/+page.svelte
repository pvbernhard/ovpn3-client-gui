<script>
  import { Command } from "@tauri-apps/api/shell";
  import Greet from "$lib/Greet.svelte";
  import ToggleButton from "$lib/ToggleButton.svelte";

  let teste = 0;

  async function handler() {
    // const ver = await new Command('ovpn3', 'version').execute();
    const cmd = await new Command("teste", "version");
    console.log("cmd");
    const ver = await cmd.execute().catch((error) => {
      console.log("error", error);
      console.log("type", typeof error);
      return 0;
    });
    console.log("version", ver);
    teste += 1;
  }

  async function getConfigsList() {
    const configs = await new Command("ovpn3", "configs-list").execute();
    const stringConfigs = configs.stdout;

    // 0: header, 1: configs, 2: empty
    const arrayConfigs = stringConfigs.split(/-+/)[1];

    const infoConfigs = [
      ...arrayConfigs.matchAll(
        /(.+)\n([\w\s:]{24})?\s*(?!\d)([\w\s:]{24})?\s*(\d+)\n((\w+\s{0,2}\.*)+)\s*(.+)/g
      ),
    ];

    console.log(infoConfigs);

    // const arrayConfigs = stringConfigs
    //   .split(/-+/)
    //   .map((x) => x.split("\n"))
    //   .flat()
    //   .map((x) => x.split(/[ ]{2,}/))
    //   .flat()
    //   .filter((x) => x.length != 0);

    // console.log("stringConfigs");
    // console.log(stringConfigs);
    // console.log("configs");
    // console.log(arrayConfigs);
  }
</script>

<h1>Welcome to My App!</h1>

<button on:click={getConfigsList}>configs-list</button>

<ToggleButton />

<div class="row">
  <a href="https://vitejs.dev" target="_blank" rel="noreferrer">
    <img src="/vite.svg" class="logo vite" alt="Vite Logo" />
  </a>
  <a href="https://tauri.app" target="_blank" rel="noreferrer">
    <img src="/tauri.svg" class="logo tauri" alt="Tauri Logo" />
  </a>
  <a href="https://kit.svelte.dev" target="_blank" rel="noreferrer">
    <img src="/svelte.svg" class="logo svelte" alt="Svelte Logo" />
  </a>
</div>

<p>{teste} Click on the Tauri, Vite, and Svelte logos to learn more.</p>

<div class="row">
  <Greet />
  <button on:click={handler}>Teste</button>
</div>

<style>
  .logo.vite:hover {
    filter: drop-shadow(0 0 2em #747bff);
  }

  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00);
  }
</style>
