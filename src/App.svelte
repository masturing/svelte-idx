<script>
    import { onMount, setContext } from "svelte";
    import Greet from "./components/Greet.svelte";
    import Popup from "./components/Popup.svelte";
    import Outer from "./components/Outer.svelte";
    import Card from "./components/Card.svelte";
    import NameList from "./components/NameList.svelte";
    import PostList from "./components/PostList.svelte";
    import TabA from "./components/TabA.svelte";
    import TabB from "./components/TabB.svelte";
    import Counter, { getTotalCount } from "./lib/Counter.svelte";

  let doubleCounter = 0
  let inputFocus
  let activeTab = TabA

  onMount(() => {
    inputFocus.focus()
  })

  function doubleIt() {
    doubleCounter += 2
  }

  const formValues = {
    name: '',
    age: null,
    desc: '',
    gender: '',
    hoby: [],
    single: false,
    skill: [],
    year: ''
  }

  function submitForm() {
    console.log(formValues)
  }

  // reactive example
  let firstName = 'Adi'
  let lastName = 'Nugroho'
  let fullNameByLet = `${firstName} ${lastName}`
  $: fullNameReactive = `${firstName} ${lastName}`

  function changeName() {
    firstName = "Budi"
    lastName = "Gunawan"
  }

  let items = [
    {
      name: "Item A",
      price: 100
    },
    {
      name: "Item B",
      price: 200
    },
    {
      name: "Item C",
      price: 300
    }
  ]
  $: total = items.reduce((acc, item) => acc + item.price, 0)

  function addItem() {
    items = [...items, {
      name: "Item D",
      price: 400
    }]
  }

  let tall = 0

  $: if(tall < 0) {
    alert("Terlalu bogel")
  } else {
    alert("To tall")
  }

  const obj = {
    name: 'Jason',
    hoby: 'COding'
  }

  setContext("token", "inicontoh")

  let showPopup = false

  function closePopup(event) {
    showPopup = false
    alert(`This is ${event.detail}`)
  }

  function handleGreet(event) {
    alert(event.detail)
  }

</script>

<main>
  <div class="card">
    <!-- <Counter /> -->
    <button on:click={doubleIt}>Count is {doubleCounter}</button>
  </div>

  <div>
    <pre>
      {JSON.stringify(formValues, null, 2)}
    </pre>
  </div>

  <div class="card">
    <h2>Form Example</h2>
    <form on:submit|preventDefault={submitForm}>
      <div>
        <label for="name">Name</label>
        <input type="text" id="name" bind:value={formValues.name} bind:this={inputFocus}>
      </div>

      <div>
        <label for="age">Age</label>
        <input type="number" id="age" bind:value={formValues.age}>
      </div>

      <div>
        <label for="desc">Description</label>
        <textarea name="desc" id="desc" bind:value={formValues.desc}></textarea>
      </div>

      <div>
        <label for="gender">Gender</label>
        <select name="gender" id="gender" bind:value={formValues.gender}>
          <option value="">Select a gender</option>
          <option value="male">Male</option>
          <option value="female">Female</option>
        </select>
      </div>

      <div>
        <label for="hoby">Hoby</label>
        <select name="hoby" id="hoby" bind:value={formValues.hoby} multiple>
          <option value="soccer">Soccer</option>
          <option value="music">Music</option>
        </select>
      </div>

      <div>
        <input type="checkbox" id="single" bind:checked={formValues.single}/>
        <label for="single">Are you single?</label>
      </div>

      <div>
        <label for="skill">Skill</label>
        <input type="checkbox" id="html" value="html" bind:group={formValues.skill}>
        <label for="html">HTML</label>
        <input type="checkbox" id="css" value="css" bind:group={formValues.skill}>
        <label for="css">CSS</label>
        <input type="checkbox" id="js" value="js" bind:group={formValues.skill}>
        <label for="js">JS</label>
        
      </div>

      <div>
        <label for="skill">Years of Experience</label>
        <input type="radio" id="0-2" value="0-2" bind:group={formValues.year}>
        <label for="0-2">0-2</label>
        <input type="radio" id="3-5" value="3-5" bind:group={formValues.year}>
        <label for="3-5">3-5</label>
        <input type="radio" id="6-10" value="6-10" bind:group={formValues.year}>
        <label for="6-10">6-10</label>
      </div>

      <div>
        <button>Submit</button>
      </div>

    </form>

    <div>
      <p>Contoh Reactive</p>
      <p>by let : {fullNameByLet}</p>
      <p>by reactive : {fullNameReactive}</p>
      <button on:click={changeName}>Change name</button>
      <br/>
      <p>Item List Rx</p>
      <p>Total : {total}</p>
      <button on:click={addItem}>Add Item</button>

      <br>
      <p>Current tall: {tall}</p>
      <button on:click={() => (tall -= 1)}>Decrease</button>
      <button on:click={() => (tall += 1)}>Increase</button>
    </div>

    <div>
      <p>Props</p>
      <Greet name="Adi" hoby="Turu"/>
      <Greet name="Helium"/>
      <Greet {...obj}/>
    </div>
  </div>

  <br>
  <button on:click={() => showPopup = true}> Show Popup</button>
     {#if showPopup}
     <Popup on:close={closePopup}/>
     {/if}
     <Outer on:greet={handleGreet} />

     <br>

     <Card>
      <div slot="header">
        <p>This is header</p>
      </div>
      <div slot="body">This is body</div>
      <div slot="footer">This is footer</div>
     </Card>

     <Card>
      <div slot="header">
        <p>This is header</p>
      </div>
      <div slot="body">This is body</div>
     </Card>

     <NameList>
      <h3 slot="hero" let:firstName let:lastName>
        {firstName} {lastName}
      </h3>
     </NameList>

     <br>
     <p>API FETCH</p>
     <PostList/>

     <br>
     <p>Tab Layout</p>
     <button on:click={() => (activeTab = TabA)}>Tab A</button>
     <button on:click={() => (activeTab = TabB)}>Tab B</button>
     <svelte:component this={activeTab}/>

     <br>
     <h1>Module Context</h1>
     <Counter/>
     <Counter/>
     <button on:click={() => {
      alert(`Total Count ${getTotalCount()}`)
     }}>Show Total</button>
</main>

<style>
  /* input + label {
    display: inline-flex;
  } */
</style>
