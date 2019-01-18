# VUE中异步加载百度地图或高德地图

### 运行项目
```shell
git clone https://github.com/aries-dp/vue-maps.git

cd vue-maps
yarn 
yarn serve

```
### 使用utils目录下的异步加载地图asyncLoadMapApi.js 单个地图使用

  高德地图下无需传递 hasCallback 参数

```vue
<template>
  <div id="maps" :style="{width, height}"></div>
</template>

<script>
// @ is an alias to /src
import MapApi from '@/utils/asyncLoadMapApi'
import { gaodeMapKey } from '@/utils/keys'
export default {
  name: 'map',
  props: {
    width: {
      type: String,
      default: '100%'
    },
    height: {
      type: String,
      default: '450px'
    }
  },
  data() {
    return {
       map: null
    }
  }
  async mounted() {
    if (!window.AMap) {
      await MapApi.loadApi(`http://webapi.amap.com/maps?v=1.4.8&key=${gaodeMapKey}`)
    }
    this.initAMap()
  },

  methods: {
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
```

  百度地图下需传递 hasCallback 参数 来接收百度地图的callback

```vue
<template>
  <div id="maps" :style="{width, height}"></div>
</template>
<script>
// @ is an alias to /src
import MapApi from '@/utils/asyncLoadMapApi'
import { baiduMapKey } from '@/utils/keys'

export default {
  name: 'map',
  props: {
    width: {
      type: String,
      default: '100%'
    },
    height: {
      type: String,
      default: '450px'
    }
  },
  data() {
    return {
       map: null
    }
  }
  async mounted() {
   
    if (!window.BMap) {
      await MapApi.loadApi(`http://webapi.amap.com/maps?v=1.4.8&key=${baiduMapKey}`, true)
    }
    window.____callback____ = this.initBMap()
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
    }
  }
}
</script>
```
  都需要在mounted 钩子使用, 地图组件需要dom下加载地图，（mounted钩子下存在dom）
### 注意
在utils文件夹中keys.js需要申请高德地图或百度地图对应的公钥

### 效果图

百度地图
<img width="100%" height="350" src="https://github.com/aries-dp/vue-maps/blob/master/md_images/%E7%99%BE%E5%BA%A6%E5%9C%B0%E5%9B%BE.png" alt="md logo">

高德地图
<img width="100%" height="350" src="https://github.com/aries-dp/vue-maps/blob/master/md_images/%E9%AB%98%E5%BE%B7%E5%9C%B0%E5%9B%BE.png" alt="md logo">


