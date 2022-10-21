<script>
    export let EventPageVis;
    export let pageData;
</script>

{#if EventPageVis}
    <div id="EventPage">
        <div id="eventText">
            <h1>{pageData.eventName}</h1>
            <h2>{pageData.eventTime}</h2>
            <p>{pageData.eventDesc}</p>
        </div>
        <div id="eventMap">

        </div>
        <div id="eventGallery">

        </div>
    </div>
{/if}

<style>
     @import url('https://api.fonts.coollabs.io/css2?family=Roboto+Mono&display=swap');

    #EventPage{
        font-family: 'Roboto Mono', monospace;
        margin-left: 160px;
    }
</style>