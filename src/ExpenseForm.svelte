<script>
    import {onMount, onDestroy,beforeUpdate,afterUpdate} from 'svelte'
    onMount(()=>{
        console.log("form has mounted");
    })
    beforeUpdate(()=>{
        console.log("form befor update");
    })
    afterUpdate(()=>{
        console.log("form after update");
    })
    
    onDestroy(()=>{
        console.log("form is hidden");
    })
    
    

  import Title from "./Title.svelte";
  export let name = "";
  export let amount;
  export let addExpense;
  export let isEditing;
  export let editExpense;
  export let handleFormClose;

  $: isEmpty = !name || !amount;

  const handleSubmit = () => {
    console.log("form submit");
    // console.log({name,amount});
    if (isEditing) {
      editExpense({ name, amount });
    } else {
      addExpense({ name, amount });
    }
    name = "";
    amount = null;
  };
</script>

<section class="form">
  <Title title="Add Expense" />
  <form class="expense-form" on:submit|preventDefault={handleSubmit}>
    <div class="form-control">
      <label for="name">Name</label>
      <input type="text" id="name" name="name" bind:value={name} />
    </div>
    <div class="form-control">
      <label for="amout">Amount</label>
      <input type="number" id="amout" bind:value={amount} />
    </div>
    {#if isEmpty}
      <p class="form-empty">please fill out all form fields.</p>
    {/if}

    <button
      type="submit"
      class="btn btn-block disabled"
      class:disabled={isEmpty}
    >
      {#if isEditing}
        Edit and Save
      {:else}
        Add Expense
      {/if}
    </button>
    <button type="button" class="close-btn" on:click={handleFormClose}>
      <i class="fas fa-times" />
      Close
    </button>
  </form>
</section>
