<script lang="ts">
  import CheckIcon from "../icons/CheckIcon.svelte";

  export let name: string;
  export let onChange: ((value: boolean) => void) | undefined = undefined;
  export let checked = false;
  export let disabled = false;

  let touched = false;
  $: {
    if (!touched) {
      touched = true;
    } else {
      onChange?.(checked);
    }
  }
</script>

<label class="container" class:disabled>
  <input {name} type="checkbox" bind:checked {disabled} tabindex="-1" />
  <span
    class="checkmark"
    class:disabled
    class:checked
    tabindex={disabled ? undefined : 0}
  >
    {#if checked}
      <CheckIcon />
    {/if}
  </span>
  {name}
</label>

<style lang="scss">
  @import "../styles/styles.scss";
  .container {
    display: flex;
    align-items: center;
    position: relative;
    padding-left: 25px;
    height: 20px;
    cursor: pointer;

    &.disabled {
      filter: opacity($disabled-opacity);
      cursor: not-allowed;
    }
  }
  input {
    position: absolute;
    display: hidden;
    cursor: pointer;
    height: 0;
    width: 0;
    &:disabled {
      cursor: not-allowed;
    }
  }
  .checkmark {
    position: absolute;
    top: 0;
    left: 0;
    height: 20px;
    width: 20px;
    background-color: $secondary-color;
    border-radius: $border-radius / 2;
    cursor: pointer;
    color: $button-text-color;
    transition: 200ms;
    border: none;
    overflow: hidden;

    &:not(.checked) {
      box-shadow: inset 0px 0px 0px 1.5px darken($secondary-color, 10%);
    }

    &.checked {
      background-color: $primary-color;
    }

    &.disabled {
      cursor: not-allowed;
    }

    &:not(.disabled, .checked):hover {
      background-color: lighten($secondary-color, 5%);
    }
    &:not(.disabled).checked:hover {
      background-color: darken($primary-color, 5%);
    }
    &:focus {
      box-shadow: 0 0 0 1px fade-out(darken($primary-color, 10%), 0.3);
    }
  }
</style>
