<template>
	<div class="our-offices">
		<div class="container">
			<div class="offices">
				<h2>Our Offices</h2>
				<div class="tabs">
					<a
						v-for="tab in coordinates"
						:key="tab.city"
						@click="activeTab = tab"
						:class="[ activeTab.city === tab.city ? 'green' : '' ]"
					>{{tab.city}}</a>
				</div>
				<div v-if="activeTab.city === 'Kyiv'">
					<h3>Global Message Services Ukraine LLC</h3>
					<p>Kyiv, Stepan Bandera, 33</p>
					<p>02066</p>
					<p>Ukraine</p>
				</div>
				<div v-if="activeTab.city === 'New York'">
					<h3>Global Message Services United States LLC</h3>
					<p>New York, Cooper Square, 20</p>
					<p>10011</p>
					<p>United States</p>
				</div>
				<div v-if="activeTab.city === 'Guangzhou'">
					<h3>Global Message Services China LLC</h3>
					<p>Guangzhou, Gaodi, 18</p>
					<p>34812</p>
					<p>China</p>
				</div>
				<div v-if="activeTab.city === 'Barcelona'">
					<h3>Global Message Services Spain LLC</h3>
					<p>Barcelona, Carrer de Ferran, 24</p>
					<p>12008</p>
					<p>Spain</p>
				</div>
			</div>
			<div class="map">
				<GoogleMap :position="position"/>
			</div>
		</div>
	</div>
</template>

<script>
  import GoogleMap from './GoogleMap.vue'

  export default {
    name: 'OurOffices',
    components: {
      GoogleMap
    },
    data() {
      return {
        activeTab: {
          city: 'Kyiv',
          position: {lat: 50.4892272, lng: 30.4876439}
				},
        coordinates: [
          {
            city: 'Kyiv',
            position: {lat: 50.4892272, lng: 30.4876439}
          },
					{
            city: 'New York',
            position: {lat: 40.7279494, lng: -73.9937221}
					},
          {
            city: 'Guangzhou',
            position: {lat: 23.1187443, lng: 113.264848}
          },
          {
            city: 'Barcelona',
            position: {lat: 41.3811666, lng: 2.1732653}
          }
				]
      }
    },
    computed: {
      position(){
        return this.activeTab.position;
      }
    }
  }
</script>

<style scoped lang="scss">
	.our-offices {
		background-color: #282828;
		color: #ffffff;

		.container {
			display: flex;
			padding: 0 0 0 60px;

			.offices {
				width: 50%;

				h2 {
					margin-top: 100px;
				}

				.tabs {
					margin-top: 45px;
					margin-bottom: 50px;

					a {
						margin-right: 20px;
						text-transform: uppercase;
						cursor: pointer;
						font-family: SuisseIntl-SemiBold;
						font-size: 11px;
						transition: all 0.5s ease-out;
					}
				}

				h3 {
					margin-bottom: 40px;
				}

				p {
					font-size: 11px;
				}
			}

			.map {
				width: 50%;
			}
		}
	}

	@media (max-width: 768px) {
		.our-offices .container {
			flex-direction: column;
			padding: 0 30px;

			.offices {
				width: 100%;

				.tabs a {
					margin-right: 10px;
					font-size: 10px;
				}

			}

			.map {
				width: 100%;
				margin-top: 50px;
				margin-bottom: 50px;
			}
		}
	}
</style>
