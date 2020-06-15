<template>
	<div>
		<city-header></city-header>
		<city-search :cities="cities"></city-search>
		<city-list 
			:cities="cities" 
			:hot="hotCities"
			:letter="letter"
			>
		</city-list>
		<city-alphaber 
			:cities="cities"
			@change="handleAlphaberChange">
		</city-alphaber>
	</div>
</template>

<script>
import CityHeader from './components/Header'
import CitySearch from './components/Search'
import CityList from './components/List'
import CityAlphaber from './components/Alphaber'
import axios from 'axios'
export default {
  name: 'City',
  components:{
  	CityHeader,
  	CitySearch,
  	CityList,
  	CityAlphaber
  },
  data () {
  	return {
  		cities: {},
  		hotCities: [],
  		letter: ''
  	}
  },
  mounted () {
  	this.getCityInfo()
  },
  methods: {
  	getCityInfo () {
  		axios.get('/api/city.json')
  			.then(this.cityGetJsonSucc)
  	},
  	cityGetJsonSucc (res) {
  		res = res.data
  		if (res.ret && res.data) {
  			const data = res.data
  			this.cities = data.cities
  			this.hotCities = data.hotCities
  		}
  	},
  	handleAlphaberChange (letter) {
  		this.letter = letter
  	}
  }
}
</script>

<style lang="stylus" scoped>

</style>
