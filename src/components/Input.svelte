<script lang="ts">
  export let value = "";
  export let prefix: string | undefined = undefined;
  export let suffix: string | undefined = undefined;
  export let placeholder: string | undefined = undefined;
  export let disabled = false;
</script>

<div class="wrapper" class:disabled>
  {#if prefix}
    <div class="prefix">{prefix}</div>
  {/if}
  <input bind:value class:prefix class:suffix {placeholder} {disabled} />
  {#if suffix}
    <div class="suffix">{suffix}</div>
  {/if}
</div>

<style lang="scss">
  @import "../styles/styles.scss";
  @import "../styles/helpers.scss";

  .wrapper {
    display: flex;
    flex-direction: row;
    align-items: stretch;
    justify-content: start;

    &.disabled {
      filter: opacity($disabled-opacity);
    }
  }
  input {
    margin: 0px;
    outline: none;
    transition: box-shadow 200ms;
    border-radius: $border-radius;
    padding-left: 0.6em;
    padding-right: 0.6em;
    padding-top: 0.4em;
    padding-bottom: 0.4em;
    z-index: 2;
    font-size: 1.1em;
    border: 1px solid $secondary-color;
    @include placeholder($secondary-color);

    &:disabled {
      cursor: not-allowed;
    }

    &:focus {
      @include box-shadow(0 0 0 2px fade-out(darken($primary-color, 10%), 0.3));
    }
    &.prefix {
      border-radius: 0px $border-radius $border-radius 0px;
      border-left: none;
    }
    &.suffix {
      border-radius: $border-radius 0px 0px $border-radius;
      border-right: none;
    }
    &.suffix.prefix {
      border-radius: 0px;
      border-left: none;
      border-right: none;
    }
  }
  div.prefix,
  div.suffix {
    background-color: $secondary-color;
    color: $secondary-button-text-color;
    display: flex;
    align-items: center;
    padding-left: 0.6em;
    padding-right: 0.6em;
    height: stretch;
  }
  div.prefix {
    border-radius: 10px 0px 0px 10px;
  }
  div.suffix {
    border-radius: 0px 10px 10px 0px;
  }
</style>
