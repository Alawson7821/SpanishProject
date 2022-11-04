<script>
    import {fade} from 'svelte/transition';
    import { createEventDispatcher } from 'svelte';
    import 'remixicon/fonts/remixicon.css';
    import './map.svelte';
    export let EventPageVis;
    export let pageData;

    const dispatch = createEventDispatcher();
    
    function backBtnClick(){
        dispatch('backBtnClick')
    }

</script>

{#if EventPageVis}
    <div id="EventPage" transition:fade on:outroend={() => dispatch('transitionEnd')}>
        <button id="backButton" on:click={backBtnClick}>
            <i class="ri-arrow-left-line"></i>
        </button>
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
    
    #backButton{
        font-size: 20px;
        padding-top: 7px;
        padding-bottom: 5px;
        padding-left: 7px;
        padding-right: 7px;
        border-color: #ffffff5e;
        border-style:solid;
        border-width: 1px;
        border-radius: 10px;
        background-color: rgba(255, 255, 255, .15);
        backdrop-filter: blur(5px);
    }

    #backButton:hover{
        background-color: rgba(255, 255, 255, .30);
    }
</style>