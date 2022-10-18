<script>
  import Timeline from "./lib/timeline.svelte";
  import EventPoster from './lib/eventPoster.svelte';
  let posterVis = false;
  let posterData;

  function timeBtnHoverHandler(event){
    posterVis = true;

    posterData = {
      eventName: event.detail.name,
      eventTime: event.detail.time,
      eventTimeBegin: event.detail.begin,
      eventTimeEnd: event.detail.end,
      eventDesc: event.detail.desc,
    }
  }
</script>

<div id="wrapper">
  <Timeline on:timeBtnHover={timeBtnHoverHandler} on:timeBtnHoverStop={() => posterVis = false}/>
  <EventPoster posterVis={posterVis} posterData={posterData}/>
</div>