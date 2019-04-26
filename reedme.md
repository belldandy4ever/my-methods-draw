# Methods-Draw 使用指南

## iframe引入示例
```
<iframe 
  title="methodDraw" 
  name="methodDraw"
  sandbox="allow-scripts allow-forms allow-same-origin" 
  src="./index.html" 
  height="800" 
  width="100%" 
  scrolling="no"
  frameBorder="0"
/>
```
---

## 等待methodDraw加载完成示例

- 此代码表示查询methodDraw相关api是否已可调用，如不能调用，50ms后再反复查询，知道可调用后，执行回调
```
function onMethodDrawReady(callback){
  if(!window.frames['methodDraw'].svgCanvas){
    setTimeout(()=>{
      onMethodDrawReady(callback)
    },50)
    return 
  }
  callback(window.frames['methodDraw'])
}
```

