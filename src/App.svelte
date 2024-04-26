<script>
  import Counter from './lib/Counter.svelte'

  let doubleCounter = 0
  function doubleIt() {
    doubleCounter += 2
  }

  const formValues = {
    name: '',
    age: null,
    desc: '',
    gender: '',
    hoby: []
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
    <form>
      <div>
        <label for="name">Name</label>
        <input type="text" id="name" bind:value={formValues.name}>
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
    </form>
  </div>

</main>

<style>
  /* input + label {
    display: inline-flex;
  } */
</style>
