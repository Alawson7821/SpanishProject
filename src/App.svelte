<script>
  import Timeline from "./lib/timeline.svelte";
  import EventPoster from './lib/eventPoster.svelte';
  import EventPage from './lib/eventPage.svelte'
  let posterVis = false;
  let eventsVisible = true;
  let EventPageVis = false;
  let highlightVis = false;

  let posterData;
  function timeBtnHoverHandler(event){
    posterVis = true;

    posterData = {
      eventName: event.detail.name,
      eventTime: event.detail.time,
      eventTimeBegin: event.detail.begin,
      eventTimeEnd: event.detail.end,
      eventDesc: event.detail.desc,
      eventTlMargin: event.detail.timelineMargin,
    }
  }

  function timeBtnHoverStopHandler(){
    posterVis = false;
    highlightVis = false;
  }

  function timeBtnClickHandler(){
    eventsVisible = false;
    posterVis = false;
  }

  function timeBtnClickHandlerPgVis(){
    EventPageVis = true;
  }

</script>

<div id="wrapper">
  <Timeline on:timeBtnHover={timeBtnHoverHandler} on:timeBtnHoverStop={timeBtnHoverStopHandler} on:timeBtnClick={timeBtnClickHandler} eventsVisible={eventsVisible} highlightVis={highlightVis} on:transitionEnd={timeBtnClickHandlerPgVis}/>
  <EventPoster posterVis={posterVis} posterData={posterData}/>
</div>

<EventPage EventPageVis={EventPageVis} pageData={posterData}/>