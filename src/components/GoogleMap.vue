<template>
	<div id="map" >

	</div>
</template>

<script>
  import {Loader} from 'google-maps';
  import googleMapStyle from '../assets/styles/googleMapStyle.json';

  export default {
    name: "GoogleMap",
		props: {
      position: Object
		},
    data() {
      return {
        map: null
      }
    },
    watch: {
      position(value) {
        this.map.setCenter(value);
      }
    },
		async mounted() {
      const options = {
        language: 'en',
        libraries: ['places']
			}
      const loader = new Loader('AIzaSyCuJQvEPFtEnnUeDksw0T1BFBW0KNL3DHM', options);

      const google = await loader.load();

      this.map = new google.maps.Map(document.getElementById('map'), {
        center: this.position,
				styles: googleMapStyle,
        zoom: 12,
      });
    }
  }
</script>

<style scoped lang="scss">
	#map {
		width: 100%;
		height: 500px;
		position: relative;

		&:after {
			content: '';
			width: 30px;
			height: 30px;
			position: absolute;
			background: #3db565;
			top: 50%;
			left: 50%;
			border-radius: 25px;
		}
	}

	@media (max-width: 767px) {
		#map {
			height: 300px!important;
		}
	}
</style>