<script>
  import ContactCard from "./ContactCard.svelte";
  import { Contact } from "./models";

  let name = "Max";
  let title = "";
  let image = "";
  let description = "";
  let formState = "empty";

  let createdContacts = [];

  $: isContactsEmpty = !createdContacts.length;

  function addContact() {
    if (
      !name.trim().length ||
      !title.trim().length ||
      !image.trim().length ||
      !description.trim().length
    ) {
      formState = "invalid";
      return;
    }
    createdContacts = [
      ...createdContacts,
      new Contact(name, title, image, description)
    ];
  }

  function deleteFirst() {
    createdContacts.shift();
    createdContacts = [...createdContacts];
  }

  function deleteLast() {
    createdContacts.pop();
    createdContacts = [...createdContacts];
  }
</script>

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>

<div id="form">
  <div class="form-control">
    <label for="userName">User Name</label>
    <input type="text" bind:value={name} id="userName" />
  </div>
  <div class="form-control">
    <label for="jobTitle">Job Title</label>
    <input type="text" bind:value={title} id="jobTitle" />
  </div>
  <div class="form-control">
    <label for="image">Image URL</label>
    <input type="text" bind:value={image} id="image" />
  </div>
  <div class="form-control">
    <label for="desc">Description</label>
    <textarea rows="3" bind:value={description} id="desc" />
  </div>
</div>

<button on:click={addContact}>Add contact card</button>
<button on:click={deleteFirst} disabled={isContactsEmpty}>Delete First</button>
<button on:click={deleteLast} disabled={isContactsEmpty}>Delete Last</button>

{#if formState === 'invalid'}
  <p>Invalid input.</p>
{:else}
  <p>Please enter some data and hit the button</p>
{/if}

{#each createdContacts as contact, i}
  <h2># {i + 1}</h2>
  <ContactCard
    userName={contact.name}
    jobTitle={contact.jobTitle}
    description={contact.desc}
    userImage={contact.imageUrl} />
{:else}
  <p>Please start adding some contacts, we found none!</p>
{/each}
