<template>
	<div>
		<div class="search">
		  	<input  v-model="keyWord" 
				  	class="search-input" 
				  	type="text" 
				  	placeholder="输入城市名字或者拼音">
		  </div>
		  <div  class="search-content" 
		  		ref="search"
				v-show="keyWord"
		  >
		  	<ul>
		  		<li class="search-item border-bottom" 
		  			v-for="item of list" 
		  			:key="item.id"
		  			@click="handleClickItem(item.name)">
		  			{{item.name}}
		  		</li>
		  		<li v-show="hasNoDate" class="search-item border-bottom">
		  			没有找到匹配数据
		  		</li>
		  	</ul>
		  </div>
	</div>
</template>

<script>
import BScroll from 'better-scroll'
import { mapState,mapMutations } from 'vuex'
export default {
  name: 'CitySearch',
  props: {
  	cities: Object
  },
  data () {
  	return {
  		keyWord: '',
  		list: [],
  		timer: null
  	}
  },
  computed: {
  	hasNoDate () {
  		return !this.list.length
  	}
  },
  watch: {
  	keyWord () {
  		if (this.timer) {
  			clearTimeout(this.timer)
  		}
  		if(!this.keyWord){
  			this.list = []
  			return
  		}	
  		var _this = this
  		this.timer = setTimeout( () => {
  			const result = []
  			for (let i in _this.cities) {
  				_this.cities[i].forEach((value) => {
  					if(value.spell.indexOf(_this.keyWord) > -1 ||
  						value.name.indexOf(_this.keyWord) > -1) {
  						result.push(value)
  					}
  				})
  			}
  			this.list = result
  		},100)
  	}
  },
  mounted () {
  	this.scroll = new BScroll(this.$refs.search)
  },
  methods: {
  	handleClickItem (city) {
  		//this.$store.commit('changeCity', city)
  		this.changeCity(city)
  		this.$router.push('/')
  	},
  	...mapMutations(['changeCity'])
  }
}
</script>

<style lang="stylus" scoped>
	@import '~styles/varibles.styl'
	.search
		padding: 0 .1rem
		height: .72rem
		background: $bgColor
		.search-input
			box-sizing: border-box
			width: 100%
			height: .62rem
			padding: 0 .1rem
			line-height: .62rem
			text-align: center
			border-radius: .06rem
			color: #666
	.search-content
		overflow: hidden
		z-index: 1
		position: absolute
		top: 1.58rem
		left: 0
		right: 0
		bottom: 0
		background: #eee
		.search-item
			line-height: .62rem
			padding-left: .2rem
			background: #fff
			color: #666
</style>
