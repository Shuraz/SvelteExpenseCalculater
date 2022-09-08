<script>
  // localStorage.setItem("tesing","hello cockies");
  //components
  import Navbar from "./Navbar.svelte";
  import Title from "./Title.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  import { setContext } from "svelte";
  import Totals from "./Totals.svelte";
  import ExpenseForm from "./ExpenseForm.svelte";
  import Modal from "./Modal.svelte";
  import { onMount,afterUpdate } from "svelte";

  //data
  import expencesData from "./expenses";

  let total = 0;

  let setName = "";
  let setAmout = null;
  let setId = null;
  //variables
  // let expenses = [...expencesData];
  let expenses = [];
  let title = "Add Expense";

  //variables to show and hide form
  let isFormShow = false;
  const handleShowForm = () => {
    return (isFormShow = true);
  };

  const handleFormClose = () => {
    isFormShow = false;
    setName = "";

    setAmout = null;

    setId = null;
  };

  //reactive

  $: isEditing = setId ? true : false;

  $: total = expenses.reduce((acc, curr) => {
    return (acc += curr.amount);
  }, 0);

  //function
  const removeExpense = (id) => {
    expenses = expenses.filter((item) => item.id !== id);
    // setLocalStorage();
  };
  const clearExpenses = () => {
    expenses = [];
    // setLocalStorage();
  };

  $: console.log({ setAmout, setName });

  const addExpense = ({ name, amount }) => {
    console.log(`value is: ${(name, amount)}`);
    let expense = { id: Math.random(), name, amount };
    expenses = [expense, ...expenses];
    // setLocalStorage();
  };

  const modifyExpense = (id) => {
    console.log("tesit eidting");
    let expense = expenses.find((item) => item.id === id);
    console.log(expense);
    setId = expense.id;
    setAmout = expense.amount;
    setName = expense.name;
    // setLocalStorage();
    handleShowForm();
  };

  const editExpense = ({ name, amount }) => {
    // console.log({name, amount});
    expenses = expenses.map((item) => {
      return item.id === setId ? { ...item, name, amount } : { ...item };
    });
    setId = null;
    setAmout = null;
    setName = "";
    // setLocalStorage();
  };

  //context

  setContext("remove", removeExpense);
  setContext("modify", modifyExpense);

  //cookies...
  const setLocalStorage=()=>{
    localStorage.setItem("expenses",JSON.stringify(expenses));
  }
  onMount(()=>{
    expenses = localStorage.getItem("expenses")
    ? JSON.parse(localStorage.getItem("expenses")):[];

  })
  afterUpdate(()=>{
    setLocalStorage();
  })
  
 
  // const getLocalStorage=()=>
  //   localStorage.getItem("expenses",);
  // }
</script>

<Navbar {handleShowForm} />
<main class="content">
  {#if isFormShow}
  <Modal>
    <ExpenseForm
      {addExpense}
      bind:name={setName}
      bind:amount={setAmout}
      {isEditing}
      {editExpense}
      {handleFormClose}
    />
    
  </Modal>
  {/if}

  <Totals title="total expenses" {total} />
  <ExpensesList {expenses} {removeExpense} {handleShowForm} />
  <button class="btn" on:click={clearExpenses}>Clear Expenses</button>
</main>

<!-- <Title {title}/> -->
