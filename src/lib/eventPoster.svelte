<script>
    import { createEventDispatcher } from 'svelte';
    import { fly } from "svelte/transition";
    export let eventName;
    export let eventTimeBegin;
    export let eventTimeEnd;
    export let eventDesc;
    export let posterVis;
    export let nextPostVis;

    const dispatch = createEventDispatcher();

</script>

{#if posterVis && nextPostVis}
    <div id="EventPoster" transition:fly="{{y:200, duration:400}}" on:outrostart={() => nextPostVis = false} on:outroend={() => nextPostVis = true}>
        <h2>{eventName}</h2>
        <h3>{eventTimeBegin - eventTimeEnd}</h3>
        <p>{eventDesc}</p>
    </div>
{/if}

<style>
    #EventPoster{
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
</style>