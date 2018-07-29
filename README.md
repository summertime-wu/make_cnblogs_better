## 食用方法

1. 首先你得有个[博客](http://www.cnblogs.com/)

2. 打开 [博客后台管理](https://i.cnblogs.com/Configure.aspx)

3. 申请js权限

4. 在博客皮肤选项卡中将博客皮肤设置为： [BlueSky](http://www.cnblogs.com/SkinUser.aspx?SkinName=BlueSky)

5. 将 [页面定制.css](https://github.com/Summertime-Wu/make_cnblogs_better/blob/master/%E9%A1%B5%E9%9D%A2%E5%AE%9A%E5%88%B6.css) 复制到 `页面定制CSS代码` 代码框内

6. 将 [页首.html](https://github.com/Summertime-Wu/make_cnblogs_better/blob/master/%E9%A1%B5%E5%B0%BE.html) 复制到 `页首Html代码` 代码框内

7. 将 [页尾.html](https://github.com/Summertime-Wu/make_cnblogs_better/blob/master/%E9%A1%B5%E5%B0%BE.html) 复制到 `页脚Html代码` 代码框内

8. 保存，即可食用

## 博客示例

------------------------>>> [夏日浅笑、](https://www.cnblogs.com/summertime-wu/p/9356736.html)

**修改前：**

![](https://images2018.cnblogs.com/blog/1138447/201807/1138447-20180723202851363-1438345274.png)

**修改后：**

![](https://images2018.cnblogs.com/blog/1138447/201807/1138447-20180723202943226-1722300911.png)

## 实现过程

### 1、顶部加载条

我采用的是[NProgress](http://ricostacruz.com/nprogress/),这个我感觉非常好用。这是他们的官网，可以直接点四个方法查看效果。

![](https://images2018.cnblogs.com/blog/1138447/201807/1138447-20180723205022194-1911954756.png)

点Download会跳到[Github](https://github.com/rstacruz/nprogress)上去，上面有详情文档和CDN地址

我采取了最简单的方法

```
$(document).ready(function(){
    NProgress.start();
    NProgress.done();
}
```

**效果是：**

![](https://images2018.cnblogs.com/blog/1138447/201807/1138447-20180723205232204-459128692.gif)


### 2、顶部导航条

顶部导航条要实现下滑隐藏，上滑加载。这个刚开始以为很难，没想到还是比较简单的。

百度找到监听滚动条事件的js方法

```
var oldScrollNum = 0;
window.onscroll = function(){
	var t = document.documentElement.scrollTop || document.body.scrollTop;
	//下滑
	if (t>oldScrollNum) {

	//上拉
	}else{

	}
	oldScrollNum = t;
}
```

然后通过这个方法改变顶部导航条的margin-top的值达到展现隐藏的效果

最后给滚动条加上过渡属性` transition: 0.5s ease-in-out;` ，这样就达到了想要的效果。

![](https://images2018.cnblogs.com/blog/1138447/201807/1138447-20180724185917290-778737027.gif)

ps：其实用CSS动画实现更流畅一点。

### 3、导航条上的关于和友情链接

这个其实就是写两篇随笔 ，因为随笔的地址是固定的所以可以写死。

![](https://images2018.cnblogs.com/blog/1138447/201807/1138447-20180723221624103-1277748915.png)

### 4、背景图片模糊

这个css3提供了原生支持：` filter: blur(3px); `

**原图：**

![](https://images2018.cnblogs.com/blog/1138447/201807/1138447-20180723211316384-2110510536.png)

**duang！加了特效后：**

![](https://images2018.cnblogs.com/blog/1138447/201807/1138447-20180723211254165-816091010.png)

### 5、为每篇文章单独的背景

这个得每篇文章里面加个隐藏域，value存背景图片的地址。

```
//设置背景图片地址
if ($("#head_bg_img").val()!=null && $("#head_bg_img").val()!="") {
	$("#myheader_bg").css("background-image","url("+$("#head_bg_img").val()+")");
}else{
	$("#myheader_bg").css("background-image","url(https://ww1.sinaimg.cn/large/0062YmUwgy1fthnpo4n7yj31hc0hrq8e.jpg)");
}
```

这里设成没有取到值就用默认的

### 6、修改markdown样式

这个就得呕心沥血的一点点调整了...

```
/** MarkDown样式调整 */
.cnblogs-markdown .hljs{
    font-size: 16px!important;
    line-height: 2!important;
    padding: 15px!important;
}
.cnblogs-markdown code{
	background:rgb(238,240,244) none !important;
	border:0px !important;
	color: rgb(73,59,92) !important;
	font-size: 16px!important;
}
.cnblogs-markdown h2{
	font-weight: 500;
	margin: 20px 0;
}
.cnblogs-markdown h2:before{
	content: "#";
	color: #eb5055;
	position: relative;
	top: 0;
	left: -12px;
}
#cnblogs_post_body h2{
	font-weight: 500;
	margin: 20px 0;
}
#cnblogs_post_body h3{
	font-size: 16px;
    font-weight: bold;
    line-height: 1.5;
    margin: 10px 0;
}
.cnblogs-markdown h3:before{
	content: "##";
	color: #2175bc;
	position: relative;
	top: 0;
	left: -8px;
}
.postBody blockquote, .postCon blockquote{
	background-image: none;
	border-left: 5px solid #DDDFE4;
	background-color: #EEF0F4;
	width: 100%;
	padding: 6px 0 6px 25px;
}

```

修改前：

![](https://images2018.cnblogs.com/blog/1138447/201807/1138447-20180723211706464-1907273889.jpg)

修改后：

![](https://images2018.cnblogs.com/blog/1138447/201807/1138447-20180723211736497-1061673885.png)

ps:感觉还是不太满意`┑(￣Д ￣)┍`


### 7、生成目录

这个采用了Github上的轮子：<https://github.com/gzdaijie/cnblogs_markdown_optimize>

然后我魔改了下。。

```
function() {
    // 根据h2、h3标签自动生成目录
    var captions_ori = $("#cnblogs_post_body h2"),
	captions_ori2 = $("#cnblogs_post_body h3"),
	captions = $("#cnblogs_post_body h2,#cnblogs_post_body h3").clone(),
	content = $("<ul id='right_meun'></ul>");
    $("#cnblogs_post_body").prepend(content.append(captions));
    var index = -1,index2 = -1;
    captions.replaceWith(function(){
	var self = this;
	if(self.tagName == "H2" || self.tagName == "h2"){
	    // 设置点击目录跳转
	    index += 1;
	    $('<a name="' + '_caption_' + index + '"></a>').insertBefore(captions_ori[index]); 
	    return '<li id="'+index+'li"><a href="#_caption_' + index + '">' + self.innerHTML + '</a><ul></ul></li>';
	} else {
		// add by summertime-wu 增加h3链接跳转
		index2 += 1;
		$('<a name="' + '_caption' + index2 + '"></a>').insertBefore(captions_ori2[index2]); 
		$("#"+index+"li ul").append("<li><a href='#_caption" + index2 + "' style='color:#5f5f5f;'>" +self.innerHTML+"</a></li>");
	    return ;
	}
    });
}
```

eummm......看起来比较糟糕，但是能跑！！

效果：

![](https://images2018.cnblogs.com/blog/1138447/201807/1138447-20180723212246854-1175418733.png)

### 8、底部导航条

这个实现和顶部的差不多，多的就是去顶尾部和上一篇下一篇的四个按钮，去顶部和去尾部用锚点很好实现，上一篇和下一篇则需要用js从页面上取值

![](https://images2018.cnblogs.com/blog/1138447/201807/1138447-20180723213141119-1220559127.png)

然后赋给自定义的按钮。

### 9、去除尾部广告

额，这个呢。实现so easy，但是有点心虚。毕竟博客园免费给我们提供的了地方写博客，然而我却......

### 10、适配手机

这个其实没有仔细处理，只是粗略的调整了下主体的大小，当浏览器宽度小于1000px时，将#main设为100%宽。

```
#main{
	width: 40%;
	background-color: white;
	/*max-width: 700px;*/
}
@media screen and (max-width: 1000px) {
	 #main {width: 100%;}
}
```

效果：

![](https://images2018.cnblogs.com/blog/1138447/201807/1138447-20180723214749933-1292994509.png)

### 11、访问统计

我这里采用的是<http://www.flagcounter.com/>,感觉挺不错的，不需要注册什么的，生成了html代码直接复制到侧边栏代码框里就可以用了。

![](https://images2018.cnblogs.com/blog/1138447/201807/1138447-20180724111919029-1418797739.png)

不过由于我把侧边栏隐藏了，所以网页上看不到。正好我也不想让这个统计影响了整体的页面风格。

当然即使隐藏了还是能够正常统计的。假如自己需要查看则需要手动在控制台改下样式，让 `#maincontent` 缩小，`#sidebar`展现。

**效果：**

![](https://images2018.cnblogs.com/blog/1138447/201807/1138447-20180724112753203-1435351605.png)


## 鸣谢

[chakhsu](https://github.com/chakhsu/pinghsu)

[gzdaijie](https://github.com/gzdaijie/cnblogs_markdown_optimize)
