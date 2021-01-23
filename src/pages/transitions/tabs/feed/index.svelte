<script>
  import { url } from "@roxi/routify";

  async function getData() {
    const res = await fetch('https://data.gov.lv/dati/lv/api/3/action/datastore_search?resource_id=d499d2f0-b1ea-4ba2-9600-2c701b03bd4a&limit=500');
    const data = await res.json()
    const result = data.result.records
    return result;
  }
</script>

<div style="padding-top: 20px">
  <h1>Covid 19 testu vēsture</h1>
</div>
{#await getData()}
    loading....
{:then records}
    {#each records.reverse() as record}
        <ul>
        <li>
      <a href={$url('./:id', {id: record._id})}>
          {record.Datums.split("T00")[0]}<br>
      </a>
        </li>
        </ul>
    {/each}
{/await}


<style>
ul{
    list-style-type: none;
    margin: 5px;
    padding: 0;
}
</style>