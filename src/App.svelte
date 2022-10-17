<script>
  import Timeline from "./lib/timeline.svelte";
  import { gradients } from "./lib/background";
  import EventPoster from './lib/eventPoster.svelte';
  import { fade } from 'svelte/transition';

  let posterVis = false;

</script>

<div id="wrapper">
  <Timeline on:timeBtnHover={() => posterVis = true} on:timeBtnHoverStop={() => posterVis = false}/>
  <EventPoster posterVis={posterVis} nextPostVis={}/>
</div>


<style>
</style>
