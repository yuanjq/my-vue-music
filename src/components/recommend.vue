<template>
	<div class="recommend" ref="recommend">
		<scroll ref="scroll" class="recommend-content" :data="discList">
			<div>
				<div v-if="recommends.length" class="slider-wrapper" ref="sliderWrapper">
					<slider>
						<div v-for="item in recommends">
							<a :href="item.linkUrl">
								<img class="needsclick" @load="loadImage" :src="item.picUrl">
							</a>
						</div>
					</slider>
				</div>
			</div>
			<div class="loading-container" v-show="!discList.length">
				<loading></loading>
			</div>
		</scroll>
	</div>
</template>

<script type="text/ecmascript-6">
	import Slider from 'base/slider'
	import Loading from 'base/loading'
	import Scroll from 'base/scroll'
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
	  			this.$refs.scroll.refresh()
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
	  	Loading,
	  	Scroll,
	  	Slider
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
		.recommend-content
			height: 100%
			overflow: hidden
			.slider-wrapper
				position: relative
				width: 100%
				overflow: hidden
			
			.loading-container
				position: absolute
				width: 100%
				top: 50%
				transform: transformY(-50%)
</style>