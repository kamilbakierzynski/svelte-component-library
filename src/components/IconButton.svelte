<script lang="ts" context="module">
  export type ButtonType = "primary" | "secondary" | "danger" | "text";
</script>

<script lang="ts">
  export let type: ButtonType = "primary";
  export let disabled = false;

  let isHoveringOverIcon = false;
  const setIsHoveringOverIcon = (val: boolean) => (isHoveringOverIcon = val);
  const entersIcon = () => setIsHoveringOverIcon(true);
  const leavesIcon = () => setIsHoveringOverIcon(false);
</script>

<div class="wrapper" on:click tabindex="0">
  <span class="icon" on:pointerenter={entersIcon} on:pointerleave={leavesIcon}>
    <slot>Button</slot>
  </span>
  <button
    tabindex="0"
    class:primary={type === "primary"}
    class:secondary={type === "secondary"}
    class:danger={type === "danger"}
    class:text={type === "text"}
    class:hover={isHoveringOverIcon}
    {disabled}
  />
</div>

<style lang="scss">
  @import "../styles/styles.scss";
  @import "../styles/helpers.scss";

  .wrapper {
    position: relative;
    overflow: hidden;
  }

  .icon {
    position: absolute;
    top: 50%;
    right: 50%;
    color: black;
    width: 20px;
    height: 20px;
    transform: translateY(-50%) translateX(50%);
    cursor: pointer;
  }

  button {
    background-color: $primary-color;
    color: $button-text-color;
    border: none;
    border-radius: $border-radius;
    padding-left: 1em;
    padding-right: 1em;
    padding-top: 1em;
    padding-bottom: 1em;
    cursor: pointer;
    transition: box-shadow 200ms, background-color 150ms;
    margin: 0.2em;
    height: 20px;
    width: 20px;

    &:disabled {
      cursor: not-allowed;
      filter: opacity($disabled-opacity);
    }

    @mixin actions($color, $hover_val: 10%, $active_val: 5%) {
      &:not([disabled]) {
        &:hover {
          background-color: lighten($color, $hover_val);
        }
        &.hover {
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
