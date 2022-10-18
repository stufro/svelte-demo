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
