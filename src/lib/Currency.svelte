<script>
  export let currency;
</script>

<style>
  .card {
    border: 2px solid #999999;
    border-radius: 20px;
    margin: 3em;
    min-width: 20%;
  }
</style>

<div class="card">
  <h3>{currency.code}</h3>
  <i>{currency.description}</i>

  <p>{currency.rate}</p>
</div>