<script>
    import { timelineEvents } from './timelineEvents';
    import { createEventDispatcher } from 'svelte';
    import { each } from 'svelte/internal';
    import { fade } from "svelte/transition";

    export let eventsVisible;
    export let highlightVis;

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

    function evDispatch(eventType, i){
        dispatch(eventType, {index: i, name: timelineEvents[i].name, time:timelineEvents[i].time, begin:timelineEvents[i].begin, eventType:timelineEvents[i].eventType, desc: timelineEvents[i].description, margin: timelineEvents[i].timelineMargin});
    }

</script>

<div id="Timeline">
    <div id="background">
        {#if highlightVis}
            <div id="highlight"></div>
        {/if}
        <div id="ticks">
            {#each timeLineTicks as {}, i}
                <div id="tick"><p id="tickText">{toYrStr(timeLineTicks[i])}</p></div>
            {/each}
        </div>
        <div id="events">
            {#if eventsVisible}
                {#each timelineEvents as { name, timelineMargin }, i}
                    <div id="TimelineEvent">
                        <button id="timelineEventButton" on:mouseenter={() => evDispatch('timeBtnHover', i)} on:mouseleave={() => dispatch('timeBtnHoverStop')} on:click={() => evDispatch('timeBtnClick', i)} transition:fade style="margin-top: {timelineMargin}px" on:outroend="{() => dispatch('transitionEnd')}">{name}</button>
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
        margin-left: 15px;
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
        margin-left: 20px;
    }

    #timelineEventButton:hover{
        background-color: rgba(255, 255, 255, .15);
    }

    #events{
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
        width: 15px;
        height: 2px;
        background-color: #ffffff;
        border-radius: 2px;
        border-width: 10px;
        margin-left: 5px;
    }

    #tickText{
        padding-top: 5px;
        font-family: 'Roboto Mono', monospace;
        padding-left: 5px;
        white-space: nowrap;

    }   

    #highlight{
        background-color: blue;
        width: 10px;
        height: 10px;
        vertical-align:top;
        display: inline-block;
        margin-left: 5px;
        margin-top: 90px;
        border-radius: 20px;
    }
</style>