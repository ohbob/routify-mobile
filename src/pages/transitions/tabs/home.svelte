<script>
    import { ready } from '@roxi/routify'
    const population = 1907675
    let result = []
    let tested = 0
    let sick = 0
    let dead = 0
    let filter = ""
    let sick_precentage
    let show_more = false
    const calculate_percentage = (partialValue, totalValue) => ((100 * partialValue) / totalValue).toFixed(2)
    const filter_collection = (collection, key, value) => collection.filter(entry => entry[key] > value).reverse()


    async function getData() {
        const res = await fetch('https://data.gov.lv/dati/lv/api/3/action/datastore_search?resource_id=d499d2f0-b1ea-4ba2-9600-2c701b03bd4a&limit=500');
        const data = await res.json()
        const result = data.result.records
        result.forEach(entry => {
            tested += entry.TestuSkaits
            sick += entry.ApstiprinataCOVID19InfekcijaSkaits
            dead += entry.MirusoPersonuSkaits
        })
        return result;
    }


    getData()
</script>


<style>
    main {
        padding-top: 50px;
        background: #7fc5bb;
        height: 100%;
        overflow: auto;
    }

</style>

<!-- routify:options index=0 -->
<main>
    <header>
        <article>
            <img src="/lv-karogs.png" alt="Latvijas karogs"/>
            <h1>SARS-CoV-2 izplatība Latvijā</h1>
            <p>Populācija uz 01.01.2020 </p>
            <p>Inficētie - {sick} / % {population} / % {calculate_percentage(sick, population)}</p>
            <p>Veiktie testi - {tested} / % {calculate_percentage(tested, population)}</p>
            <p>Nepārbaudīti - {population - tested} / % {calculate_percentage(population - tested, population)}</p>
            <p>Miruši - {dead} / % {calculate_percentage(dead, population)}</p>
            <p><small>Tiek uzskatīts, ka slimība sabiedrībā izplatās nekontrolēti, ja pozitīvo testu īpatsvars
                pārsniedz 4% robežu.</small></p>
        </article>
        <article>
            <h3>Datu avoti</h3>
            <a href="https://data.gov.lv/dati/lv/dataset/covid-19/resource/d499d2f0-b1ea-4ba2-9600-2c701b03bd4a">Covid-19
                Izmeklējumi</a>
            <a href="https://data1.csb.gov.lv/pxweb/lv/iedz/iedz__iedzskaits__ikgad/ISG010.px">Iedzīvotāju
                skaits</a>
        </article>
    </header>
</main>

