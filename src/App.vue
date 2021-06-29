<template>
  <div id="app">
    <div id="nav">
      <input type="text" placeholder="search" id="input" />
      <button id="bt" v-on:click="fetch()">search</button>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss"></style>
<script>
export default {
  data: function () {
    return {};
  },
  methods: {
    fetch() {
      var field = document.querySelector("input[id=input]").value;
      fetch(
        `https://www.mapquestapi.com/geocoding/v1/address?key=sSHcyXqUGQGnKJav2smr5rcK8MAeAHOO&location=${field}`
      )
        .then((res) => res.json())
        .then((data) => {
          let location = `${data.results[0].locations[0].latLng.lat},
            ${data.results[0].locations[0].latLng.lng}`;
          fetch(
            `https://data.climacell.co/v4/timelines?apikey=EcGPm2HkA6OceXep7AF78N3Eiaa5s0Fm&location=${location}&fields=temperature,windSpeed&timesteps=1d`
          )
            .then((innerdata) => innerdata.json())
            .then((result) => console.log(result));
        });
    },
  },
};
</script>
