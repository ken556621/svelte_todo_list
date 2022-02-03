<script>
  import Button, { Label } from "@smui/button";
  import CustomInput from "./components/Input.svelte";
  import CustomList from "./components/List.svelte";

  let ListArray = [];
  let inputValue = "";
  let currentUpdateIndex = null;
  let error = "";

  const onChange = (event) => {
    const value = event.target.value;
    inputValue = value;
    error = "";
  };

  const handleUpdate = (index) => {
    currentUpdateIndex = index;
  };

  const onUpdate = (event) => {
    const value = event.target.value;

    ListArray = ListArray.map((item, index) => {
      if (currentUpdateIndex === index) {
		item.value = value
        return item;
      }
      return item;
    });
  };

  const onDelete = (index) => {
    ListArray = ListArray.filter((item, i) => i !== index);
  };

  const onClick = () => {
    if (!inputValue) {
      error = "請輸入一些東西哦";
      return;
    }
    ListArray = [...ListArray, {
		value: inputValue,
		done: false
	}];
    inputValue = "";
  };

  const onDone = (index, isDone) => {
	ListArray = ListArray.map((item, i) => {
      if (index === i) {
		item.done = isDone
        return item;
      }
      return item;
    });
  };
</script>

<main>
  <h1>Todo List!</h1>
  <div class="wrapper">
    <CustomInput
	  inputValue={inputValue}
      onChangeCallback={onChange}
      onKeydownCallback={onClick}
    />
    <Button on:click={onClick} variant="raised">
      <Label>新增</Label>
    </Button>
  </div>
  {error}
  {#each ListArray as item, index}
    {#if currentUpdateIndex === index}
      <CustomInput
        inputValue={item.value}
        onChangeCallback={onUpdate}
        onKeydownCallback={() => currentUpdateIndex = null}
      />
	  {:else}
	    <CustomList 
		  {index} 
		  {item} 
		  {handleUpdate} 
		  {onDelete} 
		  {onDone} 
		/>
    {/if}
  	{:else}
	  There is no task today!
  {/each}
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  .wrapper {
    display: flex;
    justify-content: center;
    gap: 10px;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
