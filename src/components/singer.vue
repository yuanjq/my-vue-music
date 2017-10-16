<template>
    <div class="singer" ref="singer">
        <list-view @select="selectSinger" :data="singers" ref="list"></list-view>
    </div>
</template>

<script type="text/ecmascript-6">
    import {getSingerList} from 'api/singer'
    import {ERR_OK} from 'api/config'
    import Singer from 'common/js/singer'
    import {mapMutations} from 'vuex'

    const HOT_SINGER_LEN = 10
    const HOT_NAME = '热门'

    export default {
        data() {
            return {
                singers: []
            }
        },
        created() {
            this._getSingerList()
        },
        methods: {
            _getSingerList() {
                if (res.code === ERR_OK) {
                    this.singers = this._nomalizeSinger(res.data.list)
                }
            },
            _nomalizeSinger(list) {
                
            }
        }
    }
</script>