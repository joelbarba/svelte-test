<script lang="ts">
  import Header from '../components/Header.svelte';
  let username = 'joel.barba';
  let name = $state('Joel');
  let age = $state(30);
  function addYear() { age++ }

  let status: 'OPEN' | 'CLOSED' = $state('OPEN');
  function toggle() {
    status = status === 'OPEN' ? 'CLOSED' : 'OPEN';
  }

  type FormState = {
    firstname: string;
    lastname: string;
    age: number;
    step: number;
  };
  type FormKey = keyof FormState;

  let formState: FormState = $state({
    firstname: 'Joel',
    lastname: 'Barba',
    age: 30,
    step: 1,
  });

  let colors = $state(['red', 'green', 'blue', 'yellow', 'purple']);
</script>

<Header {username} {name}>
  <span>This is the App</span>
</Header>

{#snippet formInput({ id, labelText, type }: { id: FormKey, labelText: string, type?: string })}
  <label for={id}>
    {labelText}
    <input type={type || 'text'} bind:value={formState[id]} />
  </label>   
{/snippet}


<div class="content">
  <h1>Hello {name}!</h1>
  <p>You are {age}</p>
  <button onclick={addYear}>It is your birthday</button>

  <input type="text" bind:value={name}/>

  <p>The status is {status}</p>
  <button onclick={toggle}>Change Status</button>

  <ol>
    {#each colors as color}
      <li>{color}</li>
    {/each}
  </ol>

  <main>
    <p>Step: {formState.step}</p>

    {#if formState.step === 1}
      <div>
        <!-- <label>First Name: <input type="text" bind:value={formState.firstname} /></label> -->
        <!-- <label>Last Name:  <input type="text" bind:value={formState.lastname}  /></label> -->
        {@render formInput({ id: 'firstname', labelText: 'First Name' })}
        {@render formInput({ id: 'lastname',  labelText: 'Last Name' })}
        <button type="button" onclick={() => formState.step = 2}>Next</button>
      </div>
    {:else if formState.step === 2}
      <div>
        <label>Age: <input type="number" bind:value={formState.age} /></label>
        <button type="button" onclick={() => formState.step = 3}>Next</button>
      </div>
    {:else if formState.step === 3}
      <p>Review your information:</p>
      <p>First Name: {formState.firstname}</p>
      <p>Last Name: {formState.lastname}</p>
      <p>Age: {formState.age}</p>
      <button type="button" onclick={() => formState.step = 1}>Back</button>
    {/if}

  </main>


</div>


<style>
  .content { margin: 40px 10px; }
  button { padding: 10px 30px; }
  /* :global(div) { color: red; }
  div { color: red; } */
  
</style>