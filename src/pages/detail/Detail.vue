<template>
  <div>
  	<detail-banner :img="bannerImg" 
                   :gallaryList="gallaryImgs" 
                   :sightName="sightName">
    </detail-banner>
  	<detail-header></detail-header>
    <detail-list :list="categoryList"></detail-list>
  	<div class="content"></div>
  </div>
</template>

<script>
import DetailBanner from './components/Banner'
import DetailHeader from './components/Header'
import DetailList from './components/List'
import axios from 'axios'
export default {
  name: 'Detail',
  components: {
  	DetailBanner,
  	DetailHeader,
    DetailList
  },
  data () {
    return {
      sightName: '',
      bannerImg: '',
      categoryList: [],
      gallaryImgs: []
    }
  },
  mounted () {
    this.getDetailsInfo()
  },
  methods: {
    getDetailsInfo () {
      axios.get('/api/details.json',{
        params: {
          id: this.$route.params.id
        }
      }).then(this.handleGetDateSucc)
    },
    handleGetDateSucc (res) {
      res = res.data
      if(res.ret && res.data){
        this.sightName = res.data.sightName
        this.bannerImg = res.data.bannerImg
        this.categoryList = res.data.categoryList
        this.gallaryImgs = res.data.gallaryImgs
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
	.content
		height: 50rem
</style>
