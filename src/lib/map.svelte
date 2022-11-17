<script>
    import {regions} from './regions'
    export let mapData = {
        shownRegions: [],
        width: '',
        height: ''
    }
</script>

<div id="Map">    
    <svg height="{mapData.height}" stroke-linecap="round" stroke-linejoin="round" stroke-width=".2" width="{mapData.width}">
        {#each mapData.shownRegions as i}
            <path d="{regions[i]}"/>
            <textarea>{regions[i]}</textarea>
        {/each}
    </svg>
</div>

<div>
    <svg style="visibility: hidden;" fill="#000000" height="857" stroke="" stroke-linecap="round" stroke-linejoin="round" stroke-width=".2" width="2000">
        <circle cx="997.9" cy="189.1" id="0">
        </circle>
        <circle cx="673.5" cy="724.1" id="1">
        </circle>
        <circle cx="1798.2" cy="719.3" id="2">
        </circle>
    </svg>
</div>