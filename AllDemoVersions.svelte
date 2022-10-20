<!--
  ******************************
  1. SPLAT JSON ON SCREEN
  ******************************
-->

<script>
  let data;

  const fetchData = async () => {
    data = await fetch('https://api.coindesk.com/v1/bpi/currentprice.json')
                 .then((response) => response.json())
                 .then((json) => JSON.stringify(json, null, 1))
  }
</script>

<main>
  <div>
  <h1>DevCon - Svelte</h1>

  <div class="card">
    <button on:click={fetchData}>Fetch Bitcoin exchange rates</button>

    <pre>
      {data}
    </pre>
  </div>
</main>


<!--
  ******************************
  2. PUT CURRENCY DATA IN CARDS
  ******************************
-->

<script>
  import { current_component } from "svelte/internal";

let data;

const fetchData = async () => {
  data = await fetch('https://api.coindesk.com/v1/bpi/currentprice.json')
               .then((response) => response.json())
}
</script>

<main>
<h1>DevCon - Svelte</h1>

<div class="card">
  <button on:click={fetchData}>Fetch Bitcoin exchange rates</button>

  {#if data}
    <h2>{data.chartName} Exchange Rates</h2>
    <i>Last updated: {data.time.updated}</i>

    <div class="d-flex">
      {#each Object.values(data.bpi) as currency}
        <div class="card">
          <h3>{currency.code}</h3>
          <i>{currency.description}</i>

          <p>{currency.rate}</p>
        </div>
      {/each}
    </div>
  {/if}
</div>
</main>


<!--
  ******************************
  3. MOVE CURRENCY INTO COMPONENT
  ******************************
-->

<!-- ./src/App.svelte -->
<script>
  import { current_component } from "svelte/internal";
  import Currency from './lib/Currency.svelte'

let data;

const fetchData = async () => {
  data = await fetch('https://api.coindesk.com/v1/bpi/currentprice.json')
               .then((response) => response.json())
}
</script>

<main>
<h1>DevCon - Svelte</h1>

<div class="card">
  <button on:click={fetchData}>Fetch Bitcoin exchange rates</button>

  {#if data}
    <h2>{data.chartName} Exchange Rates</h2>
    <i>Last updated: {data.time.updated}</i>

    <div class="d-flex">
      {#each Object.values(data.bpi) as currency}
        <Currency currency={currency}/>
      {/each}
    </div>
  {/if}
</div>
</main>

<!-- ./src/lib/Currency.svelte -->
<script>
  export let currency;
</script>

<div class="card">
  <h3>{currency.code}</h3>
  <i>{currency.description}</i>

  <p>{currency.rate}</p>
</div>



<!--
  ******************************
  4. USE AWAIT TO SHOW LOADING ELEMENT
  ******************************
-->

<script>
  import Currency from './lib/Currency.svelte'

let promise;

const fetchData = () => {
  promise = fetch('https://api.coindesk.com/v1/bpi/currentprice.json')
            .then((response) => response.json())
}
</script>

<main>
<h1>DevCon - Svelte</h1>

<div class="card">
  <button on:click={fetchData}>Fetch Bitcoin exchange rates</button>

  {#if promise}
    {#await promise}
      <div class="card">
        <i>Loading...</i>
      </div>
    {:then data}
      <h2>{data.chartName} Exchange Rates</h2>
      <i>Last updated: {data.time.updated}</i>

      <div class="d-flex">
        {#each Object.values(data.bpi) as currency}
          <Currency currency={currency}/>
        {/each}
      </div>
    {:catch error}
      <h2>{error}</h2>
    {/await}
  {/if}
</div>
</main>