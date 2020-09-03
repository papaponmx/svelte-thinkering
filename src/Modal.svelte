<script>
  import { fly } from 'svelte/transition';
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();
</script>

<style lang="scss">
  .modal-bg {
    background-color: rgba(0, 0, 0, 0.8);
    bottom: 0;
    left: 0;
    position: fixed;
    right: 0;
    top: 0;
    .modal {
      background-color: white;
      padding: 20px;
      border-radius: 15px;
    }
  }

</style>

<div class="modal-bg">
  <div class="modal" transition:fly={{ y: 200 }}>
    <button on:click={() => dispatch('CLOSE_MODAL')}>close</button>
    <slot />
  </div>
</div>
