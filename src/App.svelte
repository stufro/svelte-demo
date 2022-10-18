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
