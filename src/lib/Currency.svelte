<script>
  export let currency;
</script>

<div class="card">
  <h3>{currency.code}</h3>
  <i>{currency.description}</i>

  <p>{currency.rate}</p>
</div>