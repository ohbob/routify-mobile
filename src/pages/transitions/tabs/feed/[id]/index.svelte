<script>
  export let id;
  import { url } from "@roxi/routify";

  async function getData() {
    const res = await fetch('https://data.gov.lv/dati/lv/api/3/action/datastore_search?resource_id=d499d2f0-b1ea-4ba2-9600-2c701b03bd4a&limit=500');
    const data = await res.json()
    let result = data.result.records
    return result.filter( x => x._id == id)[0];
  }

</script>

<style>
  a {
    font-size: 1.5em;
    padding: 12px 24px;
  }
  main{

  }
</style>
<main>
{#await getData()}
  loading....
{:then record}

  <p>Datums: {record.Datums.split("T00")[0]}</p>
  <p>Testi: {record.TestuSkaits}</p>
  <p>Inficētie: {record.ApstiprinataCOVID19InfekcijaSkaits}</p>
  <p>Ipatsvars: {record.Ipatsvars}</p>
  <p>Mirušie: {record.MirusoPersonuSkaits}</p>

{/await}
</main>

<br />

<a href={$url('../../home')}>Go home</a>
<a href={$url('../')}>Go back</a>
