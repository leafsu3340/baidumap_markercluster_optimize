# baidumap_markercluster_optimize
optimize baidumap Markercluster.js
# 1.优化Markercluster渲染多个聚合点性能
   [参考](http://www.cnblogs.com/lightnull/p/6184867.html)
# 2.[extends]：根据目标marker更新聚合点样式 
 - getClusters：获取所有的聚合标识实例；
 - setSearchMarkers：用于判断聚合点是否高亮的目标marker数组;
# 效果图
baidumap_markercluster_optimize/markerclusterer.gif
![img](https://github.com/leafsu3340/baidumap_markercluster_optimize/blob/master/markerclusterer.gif)
# Link
## [BMapLib.TextIconOverlay Api](http://api.map.baidu.com/library/TextIconOverlay/1.2/docs/symbols/BMapLib.TextIconOverlay.html)
## [BMapLib.MarkerClusterer Api](http://api.map.baidu.com/library/MarkerClusterer/1.2/docs/symbols/BMapLib.MarkerClusterer.html)
# Example
使用：bdmap初始化 -> 执行'MarkerClusterer_optimize.js' -> 执行'TextIconOverlay_min.js' -> 自定义TextIconOverlay方法 -> 调用MarkerClusterer类的setSearchMarkers设置目标marders数组。
```
// 自定义TextIconOverlay样式方法
 BMapLib.TextIconOverlay.prototype.setText = function (text, flag) {
   if (
     text &&
     (!this._text || this._text.toString() != text.toString())
   ) {
     this._text = text;
     this._updateText();
     this._updateCss(flag);
     this._updatePosition();
   }
 };

 BMapLib.TextIconOverlay.prototype.getStyleByText = function (
   text,
   styles,
   flag
 ) {
   if (flag) {
     return styles[1];
   }

   return styles[0];
 };

 BMapLib.TextIconOverlay.prototype._updateCss = function (flag) {
   const style = this.getStyleByText(this._text, this._styles, flag);
   this._domElement.style.cssText = this._buildCssText(style);
 };
   ```
