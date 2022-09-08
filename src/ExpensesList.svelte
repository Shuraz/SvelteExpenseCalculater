<script>
    import SectionTitle from "./Title.svelte";
    import Expense from "./Expense.svelte";
   export let expenses =[];
   export let handleShowForm;
//    export let removeExpense;
</script>
<section>
    <SectionTitle title="expense list"/>
    <ul>
        {#each expenses as expense, index}
        <!-- <Expense {...expense}{removeExpense}/> -->
        <Expense {...expense} {handleShowForm}/>
        {:else}
        <h2>No expenses added to the list.</h2>
        {/each}
</ul>

</section>