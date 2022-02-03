<script>
  export let inputValue;
  export let onChangeCallback = () => {};
  export let onKeydownCallback = () => {};
</script>

<div>
  <input
    bind:value={inputValue}
    on:input={onChangeCallback}
    on:keydown={(e) => e.key === "Enter" && onKeydownCallback()}
    placeholder="請輸入代辦事項"
  />
</div>

<style>
</style>
