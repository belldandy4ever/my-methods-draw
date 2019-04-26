# Methods-Draw 使用指南

## iframe引入示例
```
<iframe 
  title="svgEditor" 
  id="svgEditor"
  sandbox="allow-scripts allow-forms allow-same-origin" 
  src="./index.html" 
  height="800" 
  width="100%" 
  scrolling="no"
  frameBorder="0"
/>
```
---

## 等待methodDraw加载完成

```
const editor = document.getElementById("svgEditor")
editor.addEventListener('load',callback)
```

## 与SvgEditor交互说明

- 所有与SvgEditor交互均使用H5 postMessage API

- 调用SvgEditor相关功能：
```
  /*
    type: api名字
    data: 调用api时的参数
    targetOrigin: SvgEditor iframe的src地址
  */
  editor.postMessage(
    { type: String, data: Data },
    targetOrigin: String
  )

```

- 接收SvgEditor的事件:
```
window.addEventListener('message',eventListener)
```

## api功能列表
#### 假定 
    项目地址为：const origin = 'http://loaclhost:3000'
    svgEditor iframe 地址： const svgOrigion = 'http://localhost:5000'


- 设置svgEditor iframe发送信息的对象域名(通常为项目域名)
```
editor.addEventListener('load',function(){
  editor.postMessage({
    type: 'setTargetOrigion',
    data: origin
  },svgOrigion)
})
```

- 加载svg string文件
```
editor.postMessage({
  type: 'loadSvgString',
  data: 'svgString....'
},svgOrigion)
```

- 申请获取当前svgString
```
editor.postMessage({
  type: 'requestSvgString'
},svgOrigion)
```

- 获取申请的当前svgString
```
window.addEventListener('message',function(event){
  if(event.data.type === 'responseSvgString'){
    const svgString = event.data.data
  }
})
```
