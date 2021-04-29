<script lang="ts" context="module">
  export type ButtonType = "primary" | "secondary" | "danger" | "text";
</script>

<script lang="ts">
  export let type: ButtonType = "primary";
  export let disabled = false;
</script>

<button
  on:click
  class:primary={type === "primary"}
  class:secondary={type === "secondary"}
  class:danger={type === "danger"}
  class:text={type === "text"}
  {disabled}
>
  <slot>Button</slot>
</button>

<style lang="scss">
  @import "../styles/styles.scss";
  @import "../styles/helpers.scss";

  button {
    background-color: $primary-color;
    color: $button-text-color;
    border: none;
    border-radius: $border-radius;
    padding-left: 1.2em;
    padding-right: 1.2em;
    padding-top: 0.7em;
    padding-bottom: 0.7em;
    cursor: pointer;
    transition: box-shadow 200ms, background-color 150ms;

    &:disabled {
      cursor: not-allowed;
      filter: opacity($disabled-opacity);
    }

    @mixin actions($color, $hover_val: 10%, $active_val: 5%) {
      &:not([disabled]) {
        &:hover {
          background-color: lighten($color, $hover_val);
        }
        &:active {
          background-color: lighten($color, $active_val);
        }
        &:active:not(.text) {
          background-color: darken($color, $active_val);
        }
        &:focus {
          @include box-shadow(0 0 0 4px fade-out(darken($color, 10%), 0.3));
        }
      }
    }

    &.primary {
      background-color: $primary-color;
      color: $button-text-color;
      @include actions($primary-color, 3%, 3%);
    }
    &.secondary {
      background-color: $secondary-color;
      color: $secondary-button-text-color;
      @include actions($secondary-color, 5%, 5%);
    }
    &.danger {
      background-color: $danger-color;
      color: $danger-button-text-color;
      @include actions($danger-color);
    }
    &.text {
      background-color: transparent;
      color: $primary-color;
      @include actions($primary-color, 60%, 50%);
    }
  }
</style>
