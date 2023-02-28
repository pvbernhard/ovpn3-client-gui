<script lang="ts">
  /** id for the input element; default is a random UUID */
  export let id: string = crypto.randomUUID();
  export let checked: boolean = false;
</script>

<!--
@component
Toggler made up of an input and a label. Source: https://codepen.io/mallendeo/pen/QWKrEL

It can be styled with the css vars:
- --tgl-width: width of the component
- --tgl-height: height of the component
- --tgl-radius: border-radius of the component
- --tgl-bg: color of background
- --tgl-border: color of border
- --tgl-checked: color of background when checked

- Usage:
  ```tsx
  <ToggleButton bind:checked={var_tgl} --tgl-border="black" --tgl-checked="green" />
    ```
-->

<input class="tgl tgl-input" {id} type="checkbox" bind:checked />
<label class="tgl-btn" for={id} />

<style>
  .tgl-btn {
    ---tgl-bg: var(--tgl-bg, #fbfbfb);
    ---tgl-border: var(--tgl-border, #e8eae9);
    ---tgl-checked: var(--tgl-checked, #86d993);
  }

  .tgl {
    display: none;
  }
  .tgl,
  .tgl:after,
  .tgl:before,
  .tgl *,
  .tgl *:after,
  .tgl *:before,
  .tgl + .tgl-btn {
    box-sizing: border-box;
  }
  .tgl::-moz-selection,
  .tgl:after::-moz-selection,
  .tgl:before::-moz-selection,
  .tgl *::-moz-selection,
  .tgl *:after::-moz-selection,
  .tgl *:before::-moz-selection,
  .tgl + .tgl-btn::-moz-selection {
    background: none;
  }
  .tgl::selection,
  .tgl:after::selection,
  .tgl:before::selection,
  .tgl *::selection,
  .tgl *:after::selection,
  .tgl *:before::selection,
  .tgl + .tgl-btn::selection {
    background: none;
  }
  .tgl + .tgl-btn {
    outline: 0;
    display: block;
    width: var(--tgl-width, 4em);
    height: var(--tgl-height, 2em);
    position: relative;
    cursor: pointer;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }
  .tgl + .tgl-btn:after,
  .tgl + .tgl-btn:before {
    position: relative;
    display: block;
    content: "";
    width: 50%;
    height: 100%;
  }
  .tgl + .tgl-btn:after {
    left: 0;
  }
  .tgl + .tgl-btn:before {
    display: none;
  }
  .tgl:checked + .tgl-btn:after {
    left: 50%;
  }

  .tgl-input + .tgl-btn {
    background: var(---tgl-bg);
    border-radius: var(--tgl-radius, 2em);
    padding: 2px;
    transition: all 0.4s ease;
    border: 1px solid var(---tgl-border);
  }
  .tgl-input + .tgl-btn:after {
    border-radius: var(--tgl-radius, 2em);
    background: var(---tgl-bg);
    transition: left 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275),
      padding 0.3s ease, margin 0.3s ease;
    box-shadow: 0 0 0 1px rgb(0, 0, 0, 0.25), 0 2px 0 rgb(0, 0, 0, 0.1);
  }
  .tgl-input + .tgl-btn:hover:after {
    will-change: padding;
  }
  .tgl-input + .tgl-btn:active {
    box-shadow: inset 0 0 0 calc(var(--tgl-height, 2em) * 10) var(---tgl-border);
  }
  .tgl-input + .tgl-btn:active:after {
    padding-right: 0.8em;
  }
  .tgl-input:checked + .tgl-btn {
    background: var(---tgl-checked);
  }
  .tgl-input:checked + .tgl-btn:active {
    box-shadow: none;
  }
  .tgl-input:checked + .tgl-btn:active:after {
    margin-left: -0.8em;
  }
</style>
