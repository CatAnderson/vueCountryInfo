<template lang="html">
	<main>
		<h1>Country Info</h1>
		<label for="country-dropdown"></label>
		<select
			name="country-dropdown"
			id="country-dropdown"
			v-model="selectedCountryIndex"
			v-on:change="findCountryInfo()"
		>
			<option disabled value="">Select a country</option>
			<option
				v-for="(country, index) in countries"
				:key="index"
				:value="index"
				>{{ country.name }}</option
			>
		</select>
		<p>The selected country is {{ selectedCountryInfo.name }}</p>
		<!-- <country-info
			v-for="(country, index) in countries"
			:key="index"
			:country="country"
		></country-info> -->
	</main>
</template>

<script>
import CountryInfo from './components/CountryInfo.vue';

export default {
	name: 'App',
	data() {
		return {
			countries: null,
			selectedCountryIndex: null,
			selectedCountryInfo: [{ name: '' }]
		};
	},
	components: {
		'country-info': CountryInfo
	},
	mounted() {
		this.fetchCountry();
	},
	methods: {
		fetchCountry: function() {
			fetch('https://restcountries.eu/rest/v2/all')
				.then((response) => response.json())
				.then((data) => (this.countries = data));
		},
		findCountryInfo: function() {
			this.selectedCountryInfo = this.countries[
				this.selectedCountryIndex
			];
		}
	}
};
</script>

<style lang="css" scoped></style>
