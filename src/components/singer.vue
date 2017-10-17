<template>
	<div class="singer" ref="singer">
		<list-view @select="selectSinger" :data="singers" ref="list"></list-view>
	</div>
</template>

<script type="text/ecmascript-6">
	import ListView from 'base/listview'
	import {getSingerList} from 'api/singer'
	import {ERR_OK} from 'api/config'
	import Singer from 'common/js/singer'
	import {mapMutations} from 'vuex'
	import {playlistMixin} from 'common/js/mixin'

	const HOT_SINGER_LEN = 10
	const HOT_NAME = '热门'

	export default {
		mixins: [playlistMixin],
		data() {
			return {
				singers: []
			}
		},
		created() {
			this._getSingerList()
		},
		methods: {
			handlePlaylist(playlist) {
				const bottom = playlist.length > 0 ? '60px' : ''
				this.$refs.singer.style.bottom = bottom
				this.$refs.list.refresh()
			},
			selectSinger(singer) {
				this.$router.push({
					path: `/singer/${singer.id}`
				})
				this.setSinger(singer)
			},
			_getSingerList() {
				getSingerList().then(res => {
					if (res.code === ERR_OK) {
						this.singers = this._nomalizeSinger(res.data.list)
					}
				})
			},
			_nomalizeSinger(list) {
				// let map = {
				// 	hot: {
				// 		title: HOT_NAME,
				// 		items: []
				// 	}
				// } 
				// list.forEach(item, index) => {
				// 	if (index < HOT_SINGER_LEN) {
				// 		map.hot.items.push(new Singer({
				// 			name: item.Fsinger_name,
				// 			id: item.Fsinger_mid
				// 		}))
				// 	}
				// 	const key = item.Findex
					
				// }
			}
		}
	}
</script>