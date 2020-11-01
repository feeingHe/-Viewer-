# VIEWER 图片、视频附件查看器插件
# Viewer组件

说明：
#### 该组件采用UMD规范，基于swiper2开发，兼容CMD/AMD 等规范。
#### 浏览器向下兼容到IE9，可预览图片、视频；
##### 依赖文件：picture-viewer.all.min.js/viewer.css (某些规范下需要提前引入jquery)
##### 调用的方式：$(selector).picViewer(options) 返回Viewer对象。
### 1、options配置项说明
options配置项 | 类型	| 是否必须 | 默认值 | 参数说明
---|:--|:--|:--|:--
 data | Object| 是 | [] | 组件的数据源，如：<pre> [ <br>{img: ”../img/1.png”, text:”我是文字1” },  <br/>{ <br/> img:”../img/2.png”,  text:”我是文字2”,  <br/> isVideo:true, <br> videoSrc:”./video/sy.mp4” } <br>]</pre> 
 height | Number | 否 | 300 | 组件的高度值~
 width | Number | 否 | 300 | 组件的宽度值
 viewable | Boolean | 否 | true | 组件是否可点击打开大图预览
 uploadBtnText | String | 否 | “上传” | 上传按钮文字的内容【第一个按钮显示的文案】
 deleteBtnText | String | 否 | “删除该附件” | 删除按钮文字的内容【第二个按钮显示的文案】
 uploadBtnTitle | String | 否 | “上传” | 上传按钮的提示文字【第一个按钮显示的提示文案】
 deleteBtnTitle | String | 否 | “删除该附件” | 删除按钮的提示文字【第二个按钮显示的提示文案】
 hasUploadAndDeleteBtns | Boolean | 否 | true | 是否有 **上传**和 **删除** 按钮
 paginationModel | String | 否 | “point”	分页器的模式，<br/>可选值有：<br/>“point” ：分页器为 圆点模式 <br/>“image” ：分页器为 缩略图模式
 afterView | Function | 否 | null | 点击打开大图预览之后的回调方法，<br/>必须配合viewable为true时使用
 onUpload | Function | 否 | null | 点击上传按钮之后的回调 
 onDelete | Function | 否 | null | 点击删除按钮之后的回调
 swiper | Object | 否 | 默认值：<pre style="white-space:pre-wrap;">{ <br>loop: false, <br>// 循环模式选项  <br>// 如果需要分页器 <br>pagination:'.swiper-pagination',<br>paginationClickable:true, <br>// 如果需要前进后退按钮 <br>navigation: { <br>nextEl: '.swiper-button-next', <br>prevEl: '.swiper-button-prev' <br>}, <br>onSlideClick: function () {}<br>} </pre><br/> | 该配置项与swiper2的所有配置均一致，<br/>配置项比较多，<br>具体请查看swiper2的API文档， <br/>请自行百度搜索
				




### 2、Viewer对象方法说明

方法 | 参数说明
---|:--
 addItem | 新增某一项 <br> **Viewer.addItem(***index,data***)** <br>index：在索引值为index的图片后，新增某一项或者多项，索引的起始值为0。 <br> data：需要新增的数据，支持Object/Array <br>示例：<pre> Viewer.addItem(activeIndex, [{<br> img: './images/tibet-2.jpg',<br> videoSrc:'./video/sy.mp4',<br/> text: '我是img123123',<br> isVideo:true <br>}]);</pre> 
 removeItemByIndex | 删除某一项 <br> **Viewer.removeItemByIndex (***index***)** <br> index：删除索引值为 index的附件，索引的起始值为0。<br>示例：<br> ` Viewer. removeItemByIndex(3);`
 refresh | 刷新viewer组件 <br/> **Viewer.refresh (***data***)** <br/>data：此项说明参考options配置项的data说明。<br><pre> Viewer.addItem({<br/> height:500 <br/> }）;</pre> 
 getSwiper | 获取swiper对象 **Viewer.getSwiper(***callbackFn***)** <br/>callbackFn：回调的方法，swiper对象以参数返回。<br/>示例：<br/> <pre> Viewer.getSwiper(function( swiper ){<br/>   //swiper对象以参数的形式返回<br/>  //swiper对象具体用法同swiper2组件返回的对象<br>  //具体参考swiper2的官方文档，此处不再赘述<br> }）;</pre> 


### 3、Viewer调用示例
```
var viewer = $('.test').picViewer({
    height:340,
    width:500,
    viewable:true,//是否开启图片查看器
    uploadBtnText:"上传1213",
    deleteBtnText:"删除该附件223",
    uploadBtnTitle:"上传aaa",
    deleteBtnTitle:"删除该附件aa",
    hasUploadAndDeleteBtns:true,//是否有上传和删除按钮 
    paginationModel:"image", //point image
    data:[
        { img: './images/tibet-1.jpg',
            text: "我是video",
            isVideo:true,//标识video
            videoSrc:'./video/sy.mp4'
        },
{  img: './images/posx.jpg', text: 'adsad' }, 
 ],
 afterView:function(d){
        console.log(d)
 },
 onUpload:function(params){
        viewer.addItem(params.activeIndex,[{
            img: './images/tibet-2.jpg',
            videoSrc:'./video/sy.mp4',
            text: '我是img123123',
            isVideo:true
        }]);
        console.log(params)
 },
 onDelete:function(params){
        viewer.removeItemByIndex(params.activeIndex);
        viewer.getSwiper(function(swiper){
            console.log('swiper:',swiper)
        });
        viewer.refresh({
            height:200
        })

 },
 swiper:{
        // swiper2 兼容到ie9
        slidesPerView: 1,
        mode:'vertical',
        loop:false
  },
});
```
*** waao ~ ,markdown的 table 排版是个辛苦活呢，用个 star 表示你的认可吧~***
