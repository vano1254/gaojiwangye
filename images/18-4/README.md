# 地球贴图与数据

- 下载来源：Apache ECharts 官方示例 https://echarts.apache.org/examples/data-gl/asset/world.topo.bathy.200401.jpg
- 地表影像：NASA Blue Marble Next Generation（2004 年 1 月地表合成，含地形与海底地形），背景说明：https://science.nasa.gov/earth/earth-observatory/blue-marble-next-generation/
- 下载日期：2026-11-05
- earth.jpg：从原始 5400×2700 影像缩小至 2048×1024 的 JPEG 预览与本地备份。
- earth-texture.js：同一 JPEG 的 data URI 副本。页面通过本地 script 加载，以避免离线 file:// 图片作为 WebGL 纹理的跨源限制；没有远程图片请求。
- 页面使用 ECharts GL globe + scatter3D + lines3D。
- 八座城市及连接为教学示意，非真实机构合作或咨询来源。节点数量按 28/14/12/10/10/8/10/8 的固定权重分配，和当前周期总量一致。
- 浏览器无法提供 WebGL 时显示平面地表与同一城市数据，二维图表继续运行。

## 纹理刷新修复（2026-11-05）

- globe.baseTexture 使用 data URI 字符串；预加载 Image 只用来验证图片能解码。
- GL 2.1.0 的 graphicGL.loadTexture 对已缓存 Image 对象的分支不会调用启用材质纹理的回调，而每次 setTextureImage 又会先禁用纹理。旋转/定位等 setOption 更新因此使球体变白。
- 字符串缓存分支会在缓存命中后再次调用回调，避免控件更新时丢失贴图；不修改第三方库。
- 上游源码：https://github.com/ecomfe/echarts-gl/blob/2.1.0/src/util/graphicGL.js
