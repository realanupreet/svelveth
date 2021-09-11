<script>
export let col = "blue";

export let show = false;
</script>
{#if show}
<div class="backdrop" on:click|self>
<div class="model" style="background-color: {col}">
<slot></slot>
<slot name="title"></slot>
</div>
</div>
{/if}
<style>
  .backdrop {
    width: 100vw;
    height: 100vh;
    position: fixed;
    top: 0;
    padding: 4em 0;
    background-color: rgba(238, 238, 238, 0.63);
    background-blend-mode: color-burn;
  }
  .model {
    font-family: "Urbanist";
    text-align: center;
    padding: 1em;
    background-color: rgb(253, 172, 125);
    border-radius: 0.5em;
    width: max-content;
    margin: 0 auto;
    font-size: 1.3em;
  }
</style>