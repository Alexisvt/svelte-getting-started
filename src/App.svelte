<script>
  import ContactCard from "./ContactCard.svelte";

  let name = "Alexis";
  let jobTitle = "";
  let description = "";
  let age = 33;
  let userImage = "";

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
<input type="text" bind:value={name} />
<input type="text" bind:value={jobTitle} />
<input type="text" bind:value={userImage} />
<textarea
  name="description"
  id="description"
  cols="30"
  rows="10"
  bind:value={description} />

<ContactCard userName={name} {jobTitle} {description} {userImage} />
