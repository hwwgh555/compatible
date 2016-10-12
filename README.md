# compatible
lib to record compatible ways

##1.事件监听
```javascript
obj.addEventListner("click",callBack,true);//(兼容IE11,及其它现代浏览器)
//区分 click 与 onclick
obj.attachEventListener("onclick",callBack);//(兼容IE5~IE10)
//compatible way
function addEventHandler(obj,eventName,handler){
  if(document.attachEventListener){
      obj.attachEventListener('on'+eventName,handler);
  }else if(document.addEventListener){//这里是else if
      obj.addEventListener(eventName,handler,false);
  }
}
``` 

##2.事件移除
```javascript
obj.removeEventListener('click',callBack,true);//移除addEventListener
obj.detachEventListener('onclick',callBack,true);
//compatible way
function removeEventHandler(obj,eventName,handler){
  if(document.detachEventListener){
      obj.detachEventListener('on'+eventName,handler)
  }else if(document.removeEventListener){
      obj.removeEventListener(eventName,handler,false);
  }
}
```

##3.事件对象
```javascript
//compatible way
document.onclick = function(e){//不太理解
  var event = e||event;//e event
}
```

##4.阻止事件冒泡
```javascript
e.stopPropagation();//(IE9-11及其它现代浏览器)
window.event.cacelBubble = true;//(IE5 - IE8)  cancelBubble
//compatible way
function stopBubble(e){
  var e = e||window.event; 
  if(e.stopPropagation){
      e.stopPropagation();
  }else{
      window.event.cacelBubble = true;
  }
}
```

##5.阻止默认事件
```javascript
e.preventDefault();//(IE11,Chrome,Safari)
window.event.returnValue = false;//(兼容IE5 - IE10) window.event.returnValue
return false;//(兼容IE5 - IE10)
//火狐浏览器无法阻止默认事件？
//compatible way
function preDefault(e){
  var e = e||window.event;
  if(e.preventDefault){
      e.preventDeault();
  }else{
    window.event.returnValue = false;
  }
}
```

##6.事件委托
```javascript
function eventTarget(e){
  var e = e||window.event;
  var targetEle = e.target||e.srcElement;//srcElement
  return targetEle;
}
```
###以上关于 js事件方面的兼容性处理
###以上来自http://bianhua1314.blog.163.com/blog/static/2389430302014102095531384/
