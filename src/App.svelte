<script>
  //components
  import Navbar from "./Navbar.svelte";
  import Title from "./Title.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  import { setContext } from "svelte";
  import Totals from "./Totals.svelte";
  import ExpenseForm from "./ExpenseForm.svelte";

  //data
  import expencesData from "./expenses";

  let total = 0;
  //variables
  let expenses = [...expencesData];
  let title = "Add Expense";

//variables to show and hide form
let isFormShow=false;
const handleShowForm=()=>{
	return isFormShow=true;
}

const handleFormClose=()=>{	
return isFormShow=false;
}

  let setName = "";
  let setAmout = null;
  let setId = null;
  //reactive

  $: isEditing = setId ? true : false;

  $: total = expenses.reduce((acc, curr) => {
    return (acc += curr.amount);
  }, 0);

  //function
  const removeExpense = (id) => {
    expenses = expenses.filter((item) => item.id !== id);
  };
  const clearExpenses = () => {
    expenses = [];
  };

  $:console.log({setAmout,setName});
  const addExpense = ({ name, amount }) => {
    console.log(`value is: ${(name, amount)}`);
    let expense = { id: Math.random(), name, amount };
    expenses = [expense, ...expenses];
  };
  const modifyExpense = (id) => {
    console.log("tesit eidting");
    let expense = expenses.find((item) => item.id === id);
    console.log(expense);
    setId = expense.id;
    setAmout = expense.amount;
    setName = expense.name;
  };

  const editExpense=({name,amount})=>{
	// console.log({name, amount});
	expenses=expenses.map((item)=>{
		return item.id ===setId?{...item,name,amount} :{...item}
	})
	setId=null;
	setAmout=null;
	setName="";

  }
  //context

  setContext("remove", removeExpense);
  setContext("modify", modifyExpense);
</script>

<Navbar {handleShowForm} />
<main class="content"> 
	{#if isFormShow}
	<ExpenseForm {addExpense} bind:name={setName} bind:amount={setAmout} {isEditing} {editExpense} {handleFormClose}/>	
	{/if}
  <Totals title="total expenses" {total} />
  <ExpensesList {expenses} {removeExpense} {handleShowForm} />
  <button class="btn" on:click={clearExpenses}>Clear Expenses</button>
</main>
<!-- <Title {title}/> -->
