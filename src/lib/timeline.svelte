<script>
    import { timelineEvents } from './timelineEvents';
    import { createEventDispatcher } from 'svelte';
    import { each } from 'svelte/internal';
    import { fly } from "svelte/transition";

    export let eventsVisible;

    const dispatch = createEventDispatcher();

    const timeLineTicks = [-1000, -750, -500, -250, 0, 250, 500, 750, 1000, 1500, 2000];

    function toYrStr(int){
        if(int > 0){
            return int.toString() + ' C.E.'
        } else if(int < 0){
            return (int * -1).toString() + ' B.C.E.'
        } else{
            return 0
        }
    }
</script>

<div id="Timeline" style="height:100%;">
    <div id="background">
        <div id="ticks">
            {#each timeLineTicks as {}, i}
                <div id="tick"><p id="tickText">{toYrStr(timeLineTicks[i])}</p></div>
            {/each}
        </div>
        <div id="eventYears">
            {#if eventsVisible}
                {#each timelineEvents as { name, time, begin, end, lasted, eventType, description, timelineMargin }, i}
                    <div id="TimelineEvent">
                        <button id="timelineEventButton" on:mouseenter={() => dispatch('timeBtnHover', {name: name, time:time, begin:begin, end:end, lasted:lasted, eventType:eventType, desc: description})} on:mouseleave={() => dispatch('timeBtnHoverStop')} style="margin-top:{timelineMargin}" on:click={() => dispatch('timeBtnClick', {name: name, time:time, begin:begin, end:end, lasted:lasted, eventType:eventType, desc: description})} transition:fly="{{x:-400, duration:400}}">{name}</button>
                    </div>
                {/each}
            {/if}
        </div>
    </div>
</div>

<style>
    @import url('https://api.fonts.coollabs.io/css2?family=Roboto+Mono&display=swap');

    #background{
        border-color: #ffffff5e;
        border-style:solid;
        border-width: 1px;
        border-radius: 10px;
        background-color: rgba(255, 255, 255, .15);
        backdrop-filter: blur(5px);  
        float: left;
        -webkit-user-select: none;
        -ms-user-select: none;
        user-select: none;
        margin-bottom: 10px;
    }

    #ticks{
        margin-left: 10px;
        display: inline-block;
    }

    #timelineEventButton{
        font-family: 'Roboto Mono', monospace;
        border: none;
        padding-top: 10px;
        padding-bottom: 10px;
        font-size: 15px;
        background-color: rgba(0, 0, 0, 0);
        border-radius: 10px;
        text-align: center;
    }

    #timelineEventButton:hover{
        background-color: rgba(255, 255, 255, .15);
    }

    #eventYears{
        padding-left: 90px;
        margin-top: 100px;
        padding-right: 10px;
        padding-bottom: 10px;
        vertical-align:top;
        display: inline-block;
        text-align: right;
    }

    #tick{
        margin-top: 100px;
        margin-bottom: 100px;
        width: 20px;
        height: 2px;
        background-color: #ffffff;
        border-radius: 2px;
        border-width: 10px;
    }

    #tickText{
        padding-top: 5px;
        font-family: 'Roboto Mono', monospace;
        padding-left: 10px;
        white-space: nowrap;
    }   
</style>