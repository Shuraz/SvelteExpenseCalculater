<script>
    import {getContext} from "svelte";
    export let id;
    export let name="";
    export let amount=0;
    let displayAmount=false;
    // export let removeExpense;
    const removeItem=getContext("remove");
    const setModifiedExpense=getContext("modify")
    export let handleShowForm;

</script>

    <article class="single-expense">
        <div class="expense-info">
            <h2>{name}
                <button class="amount-btn" on:click={()=>{displayAmount=!displayAmount}}>
                    <i class="fas fa-caret-down"></i>
                </button>
            </h2>
        {#if displayAmount}
        <h4>amount: ${amount}</h4>
        {/if}
        </div>
        <div class="expense-buttons">
            <button class="expense-btn edit-btn" on:click={()=>{setModifiedExpense(id)}} {handleShowForm}>
                <i class="fas fa-pen"></i>
            </button>
            <!-- <button class="expense-btn delete-btn" on:click={()=>{removeExpense(id)}}> -->
            <button class="expense-btn delete-btn" on:click={()=>{removeItem(id)}}>
                <i class="fas fa-trash"></i>
            </button>
        </div>
        <!-- <h2>{id}</h2>
        <h2>{amount}</h2> -->
    </article>
