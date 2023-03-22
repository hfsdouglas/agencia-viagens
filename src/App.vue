<template>
  <TripMakerHeader></TripMakerHeader>
  <div class="d-flex justify-content-center">
    <TripMaker></TripMaker>
    <TripResults></TripResults>
  </div>
</template>

<script>
import TripMaker from './components/TripMaker.vue';
import TripMakerHeader from './components/TripMakerHeader.vue';
import TripResults from './components/TripResults.vue';

export default {
  name: 'App',
  components: {
    TripMaker, 
    TripMakerHeader,
    TripResults
  }
}
</script>

<style>
#app {
  font-family: Arial;
}
</style>
