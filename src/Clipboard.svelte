<script>
  import { onMount, tick, createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let text;
  let textareaText;
  let textarea;

  async function copy() {
    textareaText = text();
    await tick();
    textarea.select();
    document.execCommand("Copy");
    await tick();
    textarea.blur();
    textareaText = "";
    await tick();
    dispatch("copy");
  }
</script>

<style>
  textarea {
    left: -100500;
    top: -100500;
    margin: 0;
    padding: 0;
    opacity: 0;
    width: 1px;
    height: 1px;
    border: none;
    display: block;
    position: absolute;
  }
</style>

<slot {copy} />
<textarea bind:this={textarea} value={textareaText} />
