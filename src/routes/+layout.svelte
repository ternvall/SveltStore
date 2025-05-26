<script lang="ts">
  import "../app.css";
  import Header from "./Header.svelte";

  let { children } = $props();
</script>

<div class="app">
  <Header />

  <main>
    {@render children()}
  </main>

  <footer>
    <p>
      Created by <a href="https://github.com/ternvall">Niklas</a>
    </p>
  </footer>
</div>

<style>
  .app {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  main {
    flex: 1;
    display: flex;
    flex-direction: column;
    padding: 1rem;
    width: 100%;
    max-width: 128rem;
    margin: 0 auto;
    box-sizing: border-box;
  }

  footer {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 12px;
  }
</style>
