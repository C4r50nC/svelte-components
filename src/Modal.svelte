<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();
</script>

<div
  class="backdrop"
  on:click={() => dispatch('cancel')}
  on:keypress={() => {}}
></div>
<div class="modal">
  <header>
    <slot name="header" />
  </header>

  <div class="content">
    <slot />
  </div>

  <footer>
    <slot name="footer">
      <button on:click={() => dispatch('close')}>Close</button>
    </slot>
  </footer>
</div>

<style>
  .backdrop {
    padding: 1rem;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background: rgba(0, 0, 0, 0.75);
    z-index: 10;
  }

  .modal {
    padding: 1rem;
    position: fixed;
    top: 10vh;
    left: 10%;
    width: 80%;
    max-height: 80vh;
    background: white;
    border-radius: 5px;
    z-index: 100;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    overflow: scroll;
  }

  header {
    border-bottom: 1px solid #ccc;
  }
</style>
