<template>
<div>
  <div class="banner" @click="handleBannerClick">
  	<img class="banner-img" :src="img">
  	<div class="banner-info">
  		<div class="banner-title">{{sightName}}</div>
  		<div class="banner-num">
  			<span class="iconfont banner-icon">&#xe692;</span>
  			{{this.gallaryList.length}}
  		</div>
  	</div>
  </div>
  <fade-animation>
    <common-gallary :imgs="gallaryList" 
              v-show="showGallary"
              @close="handleGallyClose"
    >
    </common-gallary>
  </fade-animation>
</div>
</template>

<script>
import CommonGallary from 'common/gallary/Gallary'
import FadeAnimation from 'common/fade/FadeAnimation'
export default {
  name: 'DetailBanner',
  data () {
  	return {
  		showGallary: false
  	}
  },
  props: {
  	img: String,
  	gallaryList: Array,
  	sightName: String
  },
  components: {
  	CommonGallary,
    FadeAnimation
  },
  methods: {
  	handleBannerClick () {
  		this.showGallary = true
  	},
  	handleGallyClose () {
  		this.showGallary = false
  	}
  }
}
</script>

<style lang="stylus" scoped>
	.banner
		position: relative
		overflow:hidden
		height: 0
		padding-bottom: 55%
		.banner-img
			width: 100%
		.banner-info
			display: flex
			position: absolute
			left: 0
			right: 0
			bottom: 0
			line-height: .6rem
			color: #fff
			background-image: linear-gradient(top, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.8))
			.banner-title
				flex: 1
				font-size: .32rem
				padding: 0 .2rem
			.banner-num
				height: .32rem
				line-height: .32rem
				margin-top: .14rem
				padding: 0 .4rem
				border-radius: .2rem
				background: rgba(0, 0, 0, 0.8)
				font-size: .24rem
				.banner-icon
					margin-right: .1rem;
					font-size: .24rem
				
</style>
