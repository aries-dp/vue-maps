# 异步加载百度地图或高德地图

### 运行项目
```shell
git clone https://github.com/aries-dp/vue-maps.git

cd vue-maps
yarn 
yarn serve

```
### 使用utils目录下的异步加载地图asyncLoadMapApi.js 

  #### 高德地图下无需传递 hasCallback 参数

  ```javascript
    MapApi.loadApi(`http://api.map.baidu.com/api?v=3.0&ak=${gaodeMapKey}`)
  ```

  #### 百度地图下需传递 hasCallback 参数

  ```javascript
    MapApi.loadApi(`http://api.map.baidu.com/api?v=3.0&ak=${baiduMapKey}`, true)
  ```
  #### 都需要在mounted 钩子使用, 地图组件需要contianer dom下加载地图，（mounted钩子下存在dom）
### 注意
在utils文件夹中keys.js需要申请高德地图或百度地图对应的公钥

### 效果图

百度地图
<img width="100%" height="350" src="https://github.com/aries-dp/vue-maps/blob/master/md_images/%E7%99%BE%E5%BA%A6%E5%9C%B0%E5%9B%BE.png" alt="md logo">

高德地图
<img width="100%" height="350" src="https://github.com/aries-dp/vue-maps/blob/master/md_images/%E9%AB%98%E5%BE%B7%E5%9C%B0%E5%9B%BE.png" alt="md logo">


