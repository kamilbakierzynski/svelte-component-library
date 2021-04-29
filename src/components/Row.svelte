<script context="module" lang="ts">
  export type JustifyContent =
    | "space-between"
    | "space-around"
    | "center"
    | "space-evenly";
</script>

<script lang="ts">
  export let justifyContent: JustifyContent = "space-between";
</script>

<div
  class:space-between={justifyContent === "space-between"}
  class:space-around={justifyContent === "space-around"}
  class:center={justifyContent === "center"}
  class:space-evenly={justifyContent === "space-evenly"}
>
  <slot />
</div>

<style lang="scss">
  div {
    display: flex;
    flex-direction: row;
    align-items: center;
    margin: 1em;

    &.space-between {
      justify-content: space-between;
    }
    &.space-around {
      justify-content: space-around;
    }
    &.center {
      justify-content: center;
    }
    &.space-evenly {
      justify-content: space-evenly;
    }
  }
</style>
