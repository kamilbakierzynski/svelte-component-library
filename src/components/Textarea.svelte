<script lang="ts">
  export let value = "";
  export let rows = 2;
  export let placeholder: string | undefined = undefined;
  export let disabled = false;
</script>

<textarea bind:value {rows} {disabled} {placeholder}/>

<style lang="scss">
  @import "../styles/styles.scss";
  @import "../styles/helpers.scss";

  textarea {
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
    &::-webkit-scrollbar {
      display: none;
    }
  }
</style>
