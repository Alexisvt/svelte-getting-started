<script>
  import ContactCard from "./ContactCard.svelte";

  let name = "Alexis";
  let age = 33;

  $: uppercaseName = name.toUpperCase();

  function incrementAge() {
    age += 1;
  }

  function changeName() {
    name = "David";
  }

  function nameInput({ target }) {
    name = target.value;
  }
</script>

<style>
  h1 {
    color: purple;
  }
</style>

<h1>Hello {uppercaseName}, my age is {age}!</h1>
<button on:click={incrementAge}>Change Age</button>
<!-- <input type="text" value={name} on:input={nameInput} /> -->
<input type="text" bind:value={name} />

<ContactCard />
