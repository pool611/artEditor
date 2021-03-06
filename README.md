# artEditor
artEditor是一款基于jQuery的移动端富文本编辑器，支持插入图片
这里另起分支，专注于在webapp中使用，主要涉及的浏览器为safari和chrome，可以输入文字和插入图片的富文本框，移动端请不要附带太多复杂的编辑功能  
    
# 引用
在页面中引入下面资源 
```   
<script src="http://code.jquery.com/jquery-1.11.0.min.js"></script>  
<script src="artEditor.min.js"></script>   
```
# CDN    
artEditor cdn 加载方式：    
```   
<script src="https://unpkg.com/arteditor"></script>  
```   
# Options
### imgTar
  图片上传按钮
### limitSize
  图片最大限制，默认3兆
### showServer
  显示从服务端返回的图片，默认是显示本地资源的图片
### uploadUrl
  图片上传路劲
### data
  上传图片其他参数，例如：{type: 1}  
### uploadField
  上传图片字段, 默认值：uploadfile
### validHtml
  粘贴时，去除不合法的html标签
### uploadSuccess
  图片上传成功回调
### uploadError
  图片上传失败回调
### formInputId
  表单隐藏域id，如果设置，则编辑器内容会储存到该元素value值
### compressSize
  图片超过大小会被压缩，单位（兆）
### breaks  
  换行符，非Firefox默认为div，如果该值为true，则换行符替换为br   
### beforeUpload   
  图片上传之前的回调（function）,参数图片base64数据

# Methods

### getValue
    获取值，$('#content').getValue()
### setValue
    设置值，$('#content').setValue('<div></div>')


# Example
html:
```
<div class="article-content" id="content">
  <p><br/></p>
</div>
```
js:

```
$('#content').artEditor({
	imgTar: '#imageUpload',
	limitSize: 5,   // M
	showServer: false,
	uploadUrl: '',
	data: {},
	uploadField: 'image',
	validHtml: ["br"],
  beforeUpload: function(imgBase64) {
    // 处理完之后，必须return图片数据   
    // return imgBase64         
  },
	uploadSuccess: function(res) {
            // 这里是处理返回数据业务逻辑的地方
            // `res`为服务器返回`status==200`的`response`
            // 如果这里`return <path>`将会以`<img src='path'>`的形式插入到页面
            // 如果发现`res`不符合业务逻辑
            // 比如后台告诉你这张图片不对劲
            // 麻烦返回 `false`
            // 当然如果`showServer==false`
            // 无所谓咯
		return res.path;
	},
	uploadError: function(res) {
		//这里做上传失败的操作
        //也就是http返回码非200的时候
		console.log(res);
	}
});
```


# Release
 
      
   
   
### 项目文件说明
|- dist 项目打包结果文件夹
|- example 项目案例文件夹
|- service 项目后台数据文件夹
|- src 项目源文件

### 项目运行方式
1. `npm install`下载用来工具
2. `npm start`页面
