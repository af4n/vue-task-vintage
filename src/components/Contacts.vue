<template>
	<div class="contacts">
		<div class="container">
			<h1>Contacts</h1>
			<div class="contact">
				<div class="contact__headquarters">
					<h2><span class="green">GMS</span> Headquarters</h2>
					<div class="headquarter">
						<div class="address">
							<p>Global Message Services Ukraine LLC</p>
							<p>Bundesstrasse 5 | 3rd Floor</p>
							<p>6300 Zug</p>
							<p>Switzerland</p>
							<h3><a href="tel: +41 41 544 62 00"><span class="green">+41 41 544 62 00</span></a></h3>
						</div>
						<div class="info">
							<p>Email</p>
							<p><a href="mailto: info@gms-worldwide.com"><span class="green">info@gms-worldwide.com</span></a></p>
							<p>Send message</p>
							<p><a href="#form"><span class="green">Viber us</span></a></p>
							<p>Send form</p>
							<p><a href="#form"><span class="green">Contact us</span></a></p>
						</div>
					</div>
				</div>
				<div class="contact__support">
					<h2>Technical support <span class="green">24/7</span></h2>
					<p>GMS understands that it can be hard to follow all new technologies. We regularly provide for all our
						clients educational trainings to make your operator`s business earn more and better though our best
						practices.</p>
					<h3><a href="tel: +41 41 544 62 00"><span class="green">+41 41 544 62 00</span></a></h3>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
  export default {
    name: 'Contacts'
  }
</script>

<style scoped lang="scss">
	.contacts {
		display: flex;
		flex-direction: column;
		margin-bottom: 100px;

		.contact {
			display: flex;
			margin-top: 50px;

			&__headquarters {
				width: 50%;

				h2 {
					margin-bottom: 50px;
				}

				.headquarter {
					display: flex;

					.address {
						width: 50%;

						h3 {
							margin-top: 40px;
						}
					}

					.info {
						width: 50%;

						a {
							font-family: SuisseIntl-SemiBold;
							text-transform: uppercase;
						}
					}
				}
			}

			&__support {
				width: 50%;

				h2 {
					margin-bottom: 50px;
				}

				h3 {
					margin-top: 40px;
				}
			}
		}
	}

	@media (max-width: 768px) {
		.container {
			padding: 0 30px;
		}

		.contacts .contact {
			display: block;

			&__headquarters {
				width: 100%;
			}

			&__support {
				width: 100%;
				margin-top: 40px;
			}
		}
	}

	@media (max-width: 480px) {
		.contacts .contact__headquarters .headquarter {
			flex-direction: column;

			.address {
				width: 100%;
			}

			.info {
				width: 100%;
				margin-top: 40px;
			}
		}
	}
</style>
