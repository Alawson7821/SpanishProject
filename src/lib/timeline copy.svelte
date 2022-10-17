<script>
    import { timelineEvents } from './timelineEvents';
    import { createEventDispatcher } from 'svelte';
    import { each } from 'svelte/internal';

    const dispatch = createEventDispatcher();

    const timeLineTicks = [-1000, -750, -500, -250, 0, 250, 500, 750, 1000, 1500, 2000]

    function toYrStr(int){
        if(int >= 0){
            return int.toString() + ' C.E.'
        } else if(int < 0){
            return (int * -1).toString() + ' B.C.E.'
        }
    }
</script>

<div id="Timeline" style="height:100%;">
    <div id="background">
        <div id="eventLength"></div>
        <div id="eventYears">
            {#each timelineEvents as { begin }}
                <div id="TimelineEvent">
                    <button id="timelineEventButton" on:mouseenter={() => dispatch('timeBtnHover', begin)} on:mouseleave={() => dispatch('timeBtnHoverStop')}>{toYrStr(begin)}</button>
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
        width: 11%;
        height: 100%
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
        padding-left: 10px;
        padding-top: 12px;
        padding-right: 10px;
        padding-bottom: 10px;
    }

    #ticks{
        margin-top: 110px;
        height: 200px;
    }

    #tick{
        margin-top: 100px;
        width: 20px;
        height: 2px;
        background-color: #ffffff;
        border-radius: 2px;
        border-width: 10px;
    }   
</style>