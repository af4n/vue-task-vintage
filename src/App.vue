<template>
	<div id="app">
		<Contacts/>
		<OurOffices/>
		<ContactUs/>
	</div>
</template>

<script>
  import Contacts from "./components/Contacts";
  import OurOffices from './components/OurOffices'
  import ContactUs from "./components/ContactUs";

  export default {
    name: 'App',
    components: {
      Contacts, OurOffices, ContactUs
    }
  }
</script>

<style lang="scss">
	@import './assets/styles/fonts.scss';
	@import './assets/styles/main.scss';
</style>
