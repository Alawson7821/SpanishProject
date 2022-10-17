<script>
    import { timelineEvents } from './timelineEvents';
    import { createEventDispatcher } from 'svelte';
    import { each } from 'svelte/internal';

    const dispatch = createEventDispatcher();

    const timeLineTicks = [-1000, -750, -500, -250, 0, 250, 500, 750, 1000, 1500, 2000]

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
            {#each timelineEvents as { name, time, begin, end, lasted, eventType }}
                <div id="TimelineEvent">
                    <button id="timelineEventButton" on:mouseenter={() => dispatch('timeBtnHover', {name, time, begin, end, lasted, eventType})} on:mouseleave={() => dispatch('timeBtnHoverStop')}>{name}</button>
                </div>
            {/each}
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
        -webkit-user-select: none; /* Safari */
        -ms-user-select: none; /* IE 10 and IE 11 */
        user-select: none;
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