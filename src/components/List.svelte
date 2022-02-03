<script>
  import Button, { Label } from "@smui/button";
  export let index;
  export let handleUpdate = () => {};
  export let onDelete = () => {};
  export let onDone = () => {};
  export let item = {};
</script>

<div>
  <li>
    {#if item.done}
      👍
    {/if}
    {item.value}
    <Button on:click={() => handleUpdate(index)} variant="raised">
      <Label>修改</Label>
    </Button>
    <Button on:click={() => onDelete(index)} variant="raised">
      <Label>刪除</Label>
    </Button>
    <Button on:click={() => onDone(index, !item.done)} variant="raised">
      <Label>Done</Label>
    </Button>
  </li>
</div>

<style>
  li {
    list-style: none;
    font-size: 20px;
  }
</style>
