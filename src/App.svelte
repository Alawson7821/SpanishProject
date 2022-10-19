<script>
  import Timeline from "./lib/timeline.svelte";
  import EventPoster from './lib/eventPoster.svelte';
  import EventPage from './lib/eventPage.svelte'
  let posterVis = false;
  let posterData;

  let eventsVisible = true;

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

  function timeBtnClickHandler(event){
    eventsVisible = false;
    posterVis = false;
  }
</script>

<div id="wrapper">
  <Timeline on:timeBtnHover={timeBtnHoverHandler} on:timeBtnHoverStop={() => posterVis = false} on:timeBtnClick={timeBtnClickHandler} eventsVisible={eventsVisible}/>
  <EventPoster posterVis={posterVis} posterData={posterData}/>
  <EventPage/>
</div>