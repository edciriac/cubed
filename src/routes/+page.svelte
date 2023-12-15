<script>
  import App from '$lib/components/App.svelte'
</script>

<div>
  <App />
</div>

<style>
  :global(body) {
    margin: 0;
  }

  div {
    width: 100vw;
    height: 100vh;
    background: rgb(113, 149, 227);
    background: linear-gradient(180deg, rgb(126, 157, 223) 0%, rgb(59, 77, 118) 100%);
  }
</style>
