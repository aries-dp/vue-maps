<template>
  <div id="maps" :style="{width, height}"></div>
</template>

<script>
// @ is an alias to /src
import MapApi from '@/utils/asyncLoadMapApi'
import { baiduMapKey } from '@/utils/keys'
import { gaodeMapKey } from '@/utils/keys'
export default {
  name: 'home',
  props: {
    width: {
      type: String,
      default: '100%'
    },
    height: {
      type: String,
      default: '450px'
    },
    'map-type': {
      type: String,
      default: 'baidu'
    }
  },
  async mounted() {
    if (this.mapType === 'baidu' && !window.BMap) {
      await MapApi.loadApi(`http://api.map.baidu.com/api?v=3.0&ak=${baiduMapKey}`, true)
    } 

    if (this.mapType === 'gaode' && !window.AMap) {
      await MapApi.loadApi(`http://webapi.amap.com/maps?v=1.4.8&key=${gaodeMapKey}`)
    }

    if (this.mapType === 'baidu') {
      window.____callback____ = this.initBMap()
    } else {
      this.initAMap()
    }
   
   
  },
  methods: {
    initBMap() {
      let [defalutLng, defaultLat, zoom] = [121.621627, 38.918699, 9] //默认为大连市的经纬度
      this.map = new window.BMap.Map("maps", {minZoom: 7, maxZoom: 19, enableMapClick: false}) // 创建Map实例
      this.map.centerAndZoom(new window.BMap.Point(defalutLng, defaultLat), zoom) // 初始化地图,设置中心点坐标和地图级别。
      this.map.enableScrollWheelZoom(true) //启用滚轮放大缩小
      this.map.addEventListener('zoomend', () => {
      })
      this.map.addEventListener('moveend', () => {
      })
    },

    initAMap() {
      let [defalutLng, defaultLat, zoom] = [121.621627, 38.918699, 11] //默认为大连市的经纬度
      
      this.map = new window.AMap.Map('maps', {
        zoom: zoom,//级别
        center: [defalutLng, defaultLat],//中心点坐标
        viewMode:'3D'//使用3D视图
      })
    }
  }
}
</script>
