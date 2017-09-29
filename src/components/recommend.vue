<template>
	<div class="recommend" ref="recommend">
		<scroll ref="scroll" class="recommend-content" :data="discList">
			<div>
				<div v-if="recommends.length" class="slider-wrapper" ref="sliderWrapper">
					
				</div>
			</div>
		</scroll>
	</div>
</template>

<script type="text/ecmascript-6">
	import Loading from 'base/loading'
	import {getRecommend, getDiscList} from 'api/recommend'
	import {ERR_OK} from 'api/config'

	export default {
		data() {
			return {
				recommends: [],
				discList: []
		  }
	  },
	  created() {
	  	this._getRecommend()
	  	this._getDiscList()
	  },
	  methods: {
			loadImage() {
	  		if (!this.checkloaded) {
	  			this.checkloaded = true
	  	  }
	    },
	    _getRecommend() {
	    	getRecommend().then((res) => {
	    		if (res.code === ERR_OK) {
	    			this.recommends = res.data.slider
	    		}
	    	})
	    },
	    _getDiscList() {
	    	getDiscList().then((res) => {
	    		if (res.code === ERR_OK) {
	    			this.discList = res.data.list
	    		}
	    	})
	    }
	  },
	  components: {
	  	Loading
	  }
  }
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
	@import "~common/stylus/variable"
	
	.recommend
		position: fixed
		width: 100%
		top: 88px
		bottom: 0

			
</style>