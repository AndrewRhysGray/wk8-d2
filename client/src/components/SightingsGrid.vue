<template lang="html">
	<div id="sightingsGrid">
		<sighting v-for="sighting in sightings" :sighting="sighting" />
	</div>
</template>

<script>
import Sighting from './Sighting';
import SightingService from '../services/SightingService.js';
import { eventBus } from '../main';
export default {
	name: "sightings-grid",
	data () {
    return {
      sightings: []
    }
  },
	components: {
		'sighting': Sighting
	},
	mounted(){
    this.fetchData();
eventBus.$on('sighting-added', (sighting) => {
	console.log(sighting);
	this.sightings.push(sighting)
})
  },
  methods: {
    fetchData(){
      SightingService.getSightings()
      .then(sightings => this.sightings = sightings);
    }
  }

}
</script>

<style lang="css" scoped>
#sightingsGrid {
	display: flex;
	flex-wrap: wrap;
	justify-content: space-evenly;
}

h2 {
	padding: 0;
	margin: 0;
}


</style>
