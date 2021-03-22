<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  mounted(){
    function getLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(showPosition);
      } else {
        console.log("REJECTED")
      }
    }

    function showPosition(position) {
      console.log('Latitude: ' + position.coords.latitude);
      console.log('Longitude: ' + position.coords.longitude);
      // Geocode an address.
      const googleMapsClient = require('@google/maps').createClient({
        key: 'AIzaSyCZa69e9CfEAQFXNRowk3F0_jFihOfUwOA'
      });
      googleMapsClient.geocode({
        // address: `${position.coords.latitude},${position.coords.longitude}`
        address: "32.324722222222,-87.105277777778",
      }, function(err, response) {
        if (!err) {
          for(let i = 0; i < response.json.results.length; i+=1){
            for(let j = 0; j < response.json.results[i].address_components.length; j+=1){
              const name = (response.json.results[i].address_components[j].long_name).toLowerCase();
              if(name === 'dallas county'){
                console.log("Selma")
              }
            }
          }
        } else {
          console.log(err.requestUrl);
        }
      });
    }
    getLocation();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
