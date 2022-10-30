<script>
    import { createEventDispatcher } from 'svelte';
    import { fly } from "svelte/transition";
    export let posterVis;
    export let posterData;

    const dispatch = createEventDispatcher();

    let nextPostVis = true;

</script>

{#if posterVis && nextPostVis}
    <div id="EventPoster" transition:fly="{{y:200, duration:400}}" on:outrostart={() => nextPostVis = false} on:outroend={() => nextPostVis = true} style="margin-top: calc(({posterData.eventIndex}px * 41) + {posterData.eventTlMargin}px + 100px)">
        <h2>{posterData.eventName}</h2>
        <h3>{posterData.eventTime}</h3>
        <p>{posterData.eventDesc}</p>
    </div>
{/if}

<style>
    @import url('https://api.fonts.coollabs.io/css2?family=Roboto&display=swap');
    @import url('https://api.fonts.coollabs.io/css2?family=Roboto+Mono&display=swap');


    #EventPoster{
        font-family: 'Roboto Mono', monospace;
        border-color: #ffffff5e;
        border-style:solid;
        border-width: 1px;
        border-radius: 10px;
        background-color: rgba(255, 255, 255, .15);
        backdrop-filter: blur(5px);
        margin-left: 20px;
        width: 30%;
        height: 400px;
        float: left;
    }

    #EventPoster h2 {
        padding-left: 10px;
    }

    #EventPoster h3 {
        padding-left: 10px;
    }

    #EventPoster p {
        padding-left: 10px;
    }
</style>