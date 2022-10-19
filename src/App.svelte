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
