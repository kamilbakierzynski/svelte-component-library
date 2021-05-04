<script lang="ts">
  import CloseIcon from "../icons/CloseIcon.svelte";
  import Button from "./Button.svelte";
  import IconButton from "./IconButton.svelte";

  export let hasCloseButton = true;

  let isOpen = false;

  const open = () => (isOpen = true);
  const close = () => (isOpen = false);

  function keydown(e: KeyboardEvent) {
    e.stopPropagation();
    if (e.key === "Escape") {
      close();
    }
  }
  function modalAction(node: HTMLElement) {
    node.addEventListener("keydown", keydown);
    return {
      destroy: () => node.removeEventListener("keydown", keydown),
    };
  }
</script>

<slot name="trigger" {open}>
  <!-- fallback trigger to open the modal -->
  <Button on:click={open}>Show modal</Button>
</slot>

{#if isOpen}
  <div class="modal" use:modalAction tabindex="0">
    <div class="backdrop" on:click={close} />
    <div class="content-wrapper">
      <slot name="header">
        <div>
          <h3>Modal heading will be here</h3>
        </div>
      </slot>
      {#if hasCloseButton}
        <span class="close_icon_button">
          <IconButton type="text" on:click={close}><CloseIcon /></IconButton>
        </span>
      {/if}
      <div class="content">
        <div>
          <p>Modal content will be here</p>
        </div>
      </div>
      <div class="footer_buttons">
        <Button type="secondary" on:click={close}>Close</Button>
        <Button on:click={close}>OK</Button>
      </div>
    </div>
  </div>
{/if}

<style lang="scss">
  @import "../styles/styles.scss";

  div.modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;

    display: flex;
    justify-content: center;
    align-items: flex-start;
    opacity: 1;
    z-index: 100;
  }
  div.modal:not(:focus-within) {
    transition: opacity 0.1ms;
    opacity: 0.99;
  }
  div.backdrop {
    background-color: rgba(0, 0, 0, 0.4);
    position: absolute;
    width: 100%;
    height: 100%;
  }
  div.content-wrapper {
    z-index: 200;
    max-width: 70vw;
    min-width: 40vw;
    border-radius: $border-radius;
    background-color: white;
    overflow: hidden;
    padding: 1.5em;
    padding-bottom: 0.4em;
    padding-top: 0.4em;
    position: relative;
    margin-top: 20vh;
  }
  @media (max-width: 767px) {
    div.content-wrapper {
      max-width: 100vw;
    }
  }
  div.content {
    max-height: 50vh;
    overflow: auto;
  }
  div.footer_buttons {
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    align-items: center;
  }
  .close_icon_button {
    position: absolute;
    top: 3px;
    right: 3px;
  }
</style>
