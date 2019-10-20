# H5和CSS3笔记

## html5

### 新语义标签

- header 头部
- nav 导航
- main 主体内容
- article 文章
- aside 主体内容之外
- footer 脚部

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Title</title>
    </head>
    <body>
        <header>头部</header>
        <nav>导航</nav>
        <!-- 主体部分 -->
        <main>
            <article>左边</article>
            <aside>右边</aside>
        </main>
        <footer>底部</footer>
    </body>
</html>
```

<strong style="color:red">注意：</strong>

- 兼容性问题，IE9中会把新语义化标签解析为行内标签
- IE8或IE8以下版本不支持语义化标签，需要解决该问题，需要通过javascript创建对应的标签`document.createElement("header")`
- 引入第三方`html5shiv.min.js`文件解决兼容问题

### 表单相关

#### 新增表单type属性

- url

- email

- number

- tel

- search

- range

- color

- time

- date

- datetime-local

  ![html5-1](E:\学习笔记\Node学习\images\html5-1.png)

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Title</title>
</head>
<body>
<!-- 主体部分 -->
<main>
    <form action="">
        <!-- url验证必须合法的url地址 必须包含http://或https://  -->
        <p>URL：<input type="url"/></p>
        <!-- email 默认提供了电子邮箱的完整验证 -->
        <p>Email：<input type="email"/></p>
        <!-- tel属性主要目的不是实现验证，它本质时为了能够在移动端打开数字键盘。意味着数字键盘限制了用户只能输入数字。 简单测试：可以通过qq发送文件》》手机端使用qq接收》》使用手机浏览器查看-->
        <p>Tel：<input type="tel"/></p>
        <!--number 只能输入数字 -->
        <p>Number：<input type="number"/></p>
        <!--Search 可以提供更人性化的输入体验-->
        <p>Search：<input type="search"/></p>
        <!--range 限定范围-->
        <p>Range：<input type="range" max="100" min="50"/></p>
        <!--color 颜色拾取-->
        <p>Color：<input type="color"/></p>
        <!-- 日期相关 -->
        <!-- 时间：时分秒 -->
        <p>Time：<input type="time"/></p>
        <!-- 日期：年月日 -->
        <p>Date：<input type="date"/></p>
        <!-- 日期：年月日 时分秒-->
        <!-- <p>Datetime：<input type="datetime"/></p> 目前只有苹果 safari支持-->
        <p>Date-local：<input type="datetime-local"/></p>

        <input type="submit" value="提交">
    </form>
</main>

</body>
</html>
```

#### 新增表单其他属性

- placeholder 输入文件提醒
- autofocus 自动获取焦点
- autocomplete 已提交内容输入补全
- required 必填
- pattern  正则属性
- multiple 配合file使用时，可以多选文件。配合email使用时，可以填写多个邮箱，多个邮箱需要使用` ,`隔开
- form 表单元素外的input标签,指定form的id时，可以同步提交

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Title</title>
</head>
<body>
<!-- 主体部分 -->
<main>
    <form action="" method="post" id="myform">
        <!--  输入内容提醒、自动获取焦点、已提交过的内容输入内容自动补全、必填   -->
        <p>Placeholder：<input type="text" placeholder="请输入内容" autofocus required autocomplete="on"/></p>
        <!-- file 选择多文件  -->
        <p>Files：<input type="file" multiple/></p>
        <!-- email 多个邮箱提交  -->
        <p>Email：<input type="email" multiple/></p>
        <input type="submit" value="提交">
    </form>
    <!-- from属性 -->
    <input type="text" from="myform">
</main>

</body>
</html>
```

#### 表单新增属性datalist

目前只有chome浏览器支持，其他浏览器都不支持，不推荐使用

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Title</title>
</head>
<body>
<!-- 主体部分 -->
<main>
    <p method="post" id="myform">
        <p>
            <!-- input与datalist建立连接 list="datalist的id值"-->
            Datalist：<input type="text" name="hobbies" list="hobbies_list">
            <datalist id="hobbies_list">
                <option value="html5+css3" label="前端"></option>
                <option value="Node+vue" label="前端/后端"></option>
                <option value="php" label="后端"></option>
            </datalist>
        </p
        <p>
            <!-- input type="url"时与datalist建立连接 list="datalist的id值" option的value=""必须包含http://获取https://-->
            Datalist：<input type="url" name="hobbies" list="hobbies_list2">
            <datalist id="hobbies_list2">
                <option value="https://www.baidu.com" label="百度"></option>
                <option value="https://www.rufeike.top" label="如非客"></option>
            </datalist>
        </p>
        <input type="submit" value="提交">
    </form>
    <!-- from属性 -->
    <input type="text" from="myform">
</main>

</body>
</html>
```

#### 表单新增事件

- oninput

  监听当前元素内容的改变：只要内容改变（添加内容、删除内容），就会触发该事件

  与`onkeyup`或`onkeydown`对比，`oninput`可以监控粘贴内容的变化。

- oninvalid

  当表单验证不通过时触发

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>表单新增事件</title>
</head>
<body>
    <form>
        <p>Oninput：<input type="text" id="test"/></p>
        <p>Oninvalid：<input type="text" required id="test2" pattern="^1d{10}"/></p>
        <p><input type="submit"></p>
    </form>
    <script>
        window.onload=function(){
            document.getElementById('test').oninput=function(){
                console.log('oninput:'+this.value);
            }
            //对比onkeyup
            document.getElementById('test').onkeyup=function(){
                console.log('onkeyup:'+this.value);
            }

            //oninvalid
            document.getElementById('test2').oninvalid=function(){
                //设置默认的提示信息
                this.setCustomValidity('请输入合法的手机号！');
            }
        }
    </script>
</body>
</html>

```

#### 进度条和度量器

- 进度条

  `<progress max="100" value="50"></progress>` 

   max代表最大值，value代表当前值

- 度量器

  `<meter max="100" min="0" high="80" low="40" value="30"></meter>`

  high：规定较高的值

  low：规定较低的值

  max：最大值

  min：最小值

  value：当前进度

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div>
        <progress></progress>
    </div>
<!--
    max:最大值
    value:当前值
-->
    <div>
        <progress max="100" value="50"></progress>
    </div>

    <p>
        度量器：
        <meter min="0" max="100" high="90" low="30" value="40"></meter>
    </p>
</body>
</html>
```

#### 表单汇总案例

展示表单所有的显示共功能

![1571455575620](C:\Users\rufeike\AppData\Roaming\Typora\typora-user-images\1571455575620.png)

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Title</title>
</head>
<style>
    input{
        display:block;
        width:100%;
        border:none;
        border:1px solid #ccc;
        border-radius: 4px;
    }
</style>
<body>
<!-- 主体部分 -->
<main>
    <form action="">
        <fieldset>
            <legend>学生档案</legend>
            <!-- url验证必须合法的url地址 必须包含http://或https://  -->
            <p>URL：<input type="url"/></p>
            <!-- email 默认提供了电子邮箱的完整验证 -->
            <p>Email：<input type="email"/></p>
            <!-- tel属性主要目的不是实现验证，它本质时为了能够在移动端打开数字键盘。意味着数字键盘限制了用户只能输入数字。 简单测试：可以通过qq发送文件》》手机端使用qq接收》》使用手机浏览器查看-->
            <p>Tel：<input type="tel"/></p>
            <!--number 只能输入数字 -->
            <p>Number：<input type="number" id="number" min="0" max="100" value="30"/></p>

            <!-- 根据nubmer值设置度量 -->
            <p>
                度量Meter：
                <meter id="meter" value="30" min="0" max="100" high="90" low="30"></meter>
            </p>

            <!--Search 可以提供更人性化的输入体验-->
            <p>Search：<input type="search"/></p>
            <!--游标range 限定范围-->
            <p>Range：<input id="range" type="range" max="100" min="0" value="20"/></p>
            <!--进度条 -->
            <p>
                <progress id="progress" value="20" min="0" max="100"></progress>
            </p>

            <!--color 颜色拾取-->
            <p>Color：<input type="color"/></p>
            <!-- 日期相关 -->
            <!-- 时间：时分秒 -->
            <p>Time：<input type="time"/></p>
            <!-- 日期：年月日 -->
            <p>Date：<input type="date"/></p>
            <!-- 日期：年月日 时分秒-->
            <!-- <p>Datetime：<input type="datetime"/></p> 目前只有苹果 safari支持-->
            <p>Date-local：<input type="datetime-local"/></p>

            <input type="submit" value="提交">
        </fieldset>

    </form>
</main>
<script>
    window.onload=function(){
        //根据number值控制度量meter的变化
        document.getElementById('number').oninput=function(){
            var value = this.value;
            document.getElementById('meter').value=value;
        }

        //根据range的值，控制进度条progress的值
        document.getElementById('range').oninput=function(){
            var value= this.value;
            document.getElementById('progress').value=value;
        }

    }
</script>
</body>
</html>

```

### 媒体标签

#### audio 音频 

标签属性：

- src
- controls
- autoplay
- loop 

#### video 视频

标签属性：

- src
- controls
- autoplay
- loop 
- width
- height
- poster

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>音频和视频文件</title>
</head>
<body>
    <!-- audio 音频
        src: 播放文件路径
        controls：音频播放控制面板
        autoplay:音频自动播放
        loop:循环播放
    -->
    <audio src="./public/media/1.mp3" controls autoplay loop></audio>
    <!-- video 音频
        src: 播放文件路径
        controls：音频播放控制面板
        autoplay:音频自动播放
        loop:循环播放
        width：宽度
        height：高度
        poster:当前视频还没有完全下载或者用户没有点击前，显示的封面。默认显示的时视频第一帧图片
        注意：
            设置高度或宽度时，只需要设置其中一个即可，会等比例缩放
    -->
    <video src="./public/media/1.mp4" controls width="200px"></video>
    <!-- 兼容不同浏览器写法-->
    <video controls width="200px">
        <source src="./public/media/1.mp4"></source>
    </video>
</body>
</html>
```

- video/audio对象常用属性
  - currentTime 视频/音频当前进度（时间）
  - duration 视频/音频的总时间（秒）
  - paused 视频的播放状态
- video/audio对象常用方法
  - play() 播放
  - pause() 暂停
  - load() 重新加载

- video/audio对象常用事件
  - oncanplay 事件在用户可以开始播放视频/音频时触发
  - ontimeupdate 该事件可以动态获取当前播放的进度
  - onended 播放完毕时触发--重置使用



### 新增js属性

#### 获取DOM元素

html5中新增的获取元素的选择

- document.querySelector("元素|类名|id") 获取单个
- document.queryAll("元素|类名|id") 获取多个

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <ul>
        <li>通过元素获取</li>
        <li class="red">通过类获取</li>
        <li id="c">C++</li>
        <li id="php">PHP</li>
    </ul>

    <script>
        window.onload=function(){
            //通过元素获取单个
            var f1=document.querySelector('li');
            console.log(f1);
            //通过class获取元素单个
            var f2=document.querySelector('.red');
            console.log(f2);
            //通过id获取元素单个
            var f3=document.querySelector('#c');
            console.log(f3);

            //获取多个
            var f4 = document.querySelectorAll('li');
            console.log(f4);

        }
    </script>
</body>
</html>


```

#### 类样式操作

- .classList.add()	添加类
- .classList.remove() 移除类
- .classList.toggle() 切换类显示和隐藏
- .classList.contain() 是否包含类

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        ul li{
            list-style: none;
            float:left;
            width:100px;
            height: 100px;
            margin-left:15px;
            border:1px solid #cccccc;
        }
        ul:after{
            display: block;
            content:'';
            clear:both;
        }
        input{
           margin:15px;
        }

        .red{
            background-color: #ff0000;
        }

        .green{
            background-color: #00ff00;
        }

        .blue{
            background-color:#0000ff;
        }

    </style>
</head>
<body>
    <main>
        <ul>
            <li></li>
            <li class="green"></li>
            <li class="blue"></li>
            <li class="red"></li>
        </ul>
        <div>
            <input type="button" value="第1个元素添加red样式" id="add">
            <input type="button" value="第2个元素移除green样式" id="remove">
            <input type="button" value="第3个元素blue样式切换" id="toggle">
            <input type="button" value="判断第4个元素是否存在red样式" id="contain">
        </div>
    </main>
    <script>
        window.onload=function(){
            //增加
            document.querySelector('#add').onclick=function(){
                document.querySelector('li').classList.add("red");
            }

            //移除
            document.querySelector('#remove').onclick=function(){
                document.querySelector('.green').classList.remove('green');
            }

            //切换
            document.querySelector('#toggle').onclick=function(){
                document.querySelectorAll('li')[2].classList.toggle('blue');
            }

            //判断
            document.querySelector('#contain').onclick=function(){
                var ret=document.querySelectorAll('li')[3].classList.contains('red');
                alert(ret);
            }

        }
    </script>
</body>
</html>
```

#### 自定义属性

- 定义：`data-属性`

- 规范：

  - 与`data-`开头
  - 名称应该都使用小写--不要包含任何大写字符
  - 名称中不应包含特殊字符
  - 名称不要使用纯数字

- 取值：

  `document.querySelector("p").dataset["camel驼峰命名"];`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <main>
        <p data-user-name="rufeike">如非客课学习</p>
    </main>
    <script>
        window.onload=function(){
            // 获取对象
            var p = document.querySelector('p');
            //取值 把data-后的单词使用camel驼峰命名法连接
            var value = p.dataset["userName"];
            console.log(value);
        }
    </script>
</body>
</html>

```

### 接口

#### 网络监听接口

- ononline 网络连通时触发接口
- onoffline 网络端口时触发接口

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<script>
    //网络联通时触发
    window.addEventListener("online",function(){
       alert('网络联通啦');
    })

    //网络断开时触发
    window.addEventListener("offline",function(){
       alert("网络断开啦");
    })
</script>
</body>
</html>
```



#### 全屏接口

- requestFullScreen() 全屏

- cancelFullScreen() 取消全屏

- fullScreenElement 是否全屏

- 注意：不同浏览器，需要添加不同前缀

  - chome:webkit

  - firefox:moz

  - ie:ms

  - opera:o

    

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        #show_box{
            border:2px solid #eaeaea;
            height: 300px;
            width:80%;
            margin:20px auto;
            background-color: #cccccc;
        }

    </style>
</head>
<body>
    <main id="show_box">
        <div class="show_content"></div>
        <div class="tool_box">
            <button id="full">全屏</button>
            <button id="cancelFull">取消全屏</button>
            <button id="isFull">是否全屏</button>
        </div>
    </main>

    <script>
        window.onload=function(){
            //设置全屏
            document.querySelector('#full').onclick=function(){
                var box=document.querySelector('#show_box');
                if(box.requestFullScreen){
                    box.requestFullscreen();
                }else if(box.webkitRequestFullScreen){//chome
                    box.webkitRequestFullScreen();
                }else if(box.mozRequestFullScreen){//fox
                    box.mozRequestFullScreen();
                }else if(box.msRequestFullScreen){//ie
                    box.msRequestFullScreen();
                }else if(box.oRequestFullScreen){//opera
                    box.oRequestFullScreen();
                }
            }

            //取消全屏
            //注意：退出全屏时，只有通过document来引用
            document.querySelector('#cancelFull').onclick=function(){
                if(document.cancelFullScreen){
                    document.cancelFullScreen();
                }else if(document.webkitCancelFullScreen){//chome
                    document.webkitCancelFullScreen();
                }else if(document.mozCancelFullScreen){//fox
                    document.mozCancelFullScreen();
                }else if(document.msCancelFullScreen){//ie
                    document.msCancelFullScreen();
                }else if(document.oCancelFullScreen){//opera
                    document.oCancelFullScreen();
                }
            }

            //判断是否全屏
            document.querySelector('#isFull').onclick=function(){
                //注意：只有fox下 fullScreenElent 严格遵守驼峰命名
                var flag = document.fullscreenElement || document.webkitFullscreenElement ||document.mozFullScreenElement ||document.msFullscreenElement ||document.oFullscreenElement;
                if(flag){
                   alert('全屏状体');
                }else{
                    alert('非全屏状体');
                }
            }

        }
    </script>
</body>
</html>


```

#### FileReader文件读取接口

- onabort 读取文件中断时触发
- onerror 读取文件出错时触发
- onload 读取文件完成时触发
- onloadend  读取完成时触发，无论成功还是失败
- onloadstart 开始读取时触发
- onprogress 读取文件过程中持续触发

- readAsText()：读取文本文件（可以使用txt打开的文件），返回文本字符串，默认编码为utf-8

- readAsBinaryString()：读取任意类型的文件，返回二进制字符。这个方法一般不是用来读取文件展示，而是存储文件。如读取文件，获取二进制数据，传递到后台，后台接收数据后在存储为文件。

- readAsDataURL()：把资源转换为base64编码的字符串，并且把这些内容直接存储在url达到优化网站的加载速度和执行效率

- abort()：中断读取

  

  图片即时预览案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        #show_box {
            height: 150px;
        }
    </style>
</head>
<body>
<main>
    <form action="" enctype="multipart/form-data">
        <p>
            选择图片：
            <input type="file" name="file" id="file"/>
        </p>
        <p>
            <img src="" alt="" id="show_box">
        </p>
        <p>
            <input type="submit" value="提交">
        </p>
    </form>
</main>
<script>
    window.onload = function () {
        document.querySelector('#file').oninput = function () {
            var files = this.files;//值为数组
            var reader = new FileReader();
            /**
             * readAsDataURL 需要传递一个文件 (图片或其他可以嵌入文档的文件）
             */
            reader.readAsDataURL(files[0]);
            reader.onload = function () {
                document.querySelector('#show_box').src = reader.result;
            }

        }
    }
</script>
</body>
</html>

```



#### 拖拽接口

- 拖拽前提

  需要为拖拽的元素添加`draggable=”true"`属性，图片和超链接默认就可以拖拽

- 被拖拽元素上的方法
  - ondrag  整个拖拽过程都会调用
  - ondragstart 当拖拽开始时调用
  - ondragleave 当鼠标离开拖拽元素位置时调用 
  - ondragend 当拖拽结束时调用
- 拖拽目标元素上的方法
  - ondragenter 当拖拽运输进入时调用
  - ondragover 当停留在目标元素上时调用
  - ondrop 单在目标元素上松开鼠标时调用
  - ondragleave 当鼠标离开目标元素时调用
- 注意：
  - <span style="color:red">如果需要触发ondrop事件，就必须在ondragover事件中阻止默认行为 `e.preventDefault()`</span>

#### 地理位置接口

#### 接口案例

##### 五子棋案例

主要练习拖拽接口

- 效果图片

  ![五子棋效果图片](https://img-blog.csdnimg.cn/2019102015152262.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3J1ZmVpa2U=,size_16,color_FFFFFF,t_70)

- 资源图片

![chessboard](E:\web\html+css3\笔记\images\chessboard.jpg)

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>五子棋</title>
    <style>
        *{padding:0;margin:0px;box-sizing: border-box;}
        body{min-width: 900px;}
        header{height:120px;background-color: #999999}
        header h3{line-height: 120px;text-align: center}
        main{}
        aside{float:left;width:120px;background-color: orange;height:500px;}
        article{margin-left:120px;height: 500px;}
        footer{width:100%;height:80px;background-color: #cccccc;min-width:900px;}
        footer p{text-align: center;line-height: 80px}

        /*棋子*/
        .chess_box{
            width:100px;
            height: 100px;
            margin:25px auto;
            -moz-user-select:none; /* Firefox私有属性 */
            -webkit-user-select:none; /* WebKit内核私有属性 */
            -ms-user-select:none; /* IE私有属性(IE10及以后) */
            -khtml-user-select:none; /* KHTML内核私有属性 */
            -o-user-select:none; /* Opera私有属性 */
            user-select:none; /* CSS3属性 */
        }
        .chess{
            position:relative;
            width:30px;
            height: 30px;
            background-color: #333;
            radial-gradient(10px 10px at 15px 15px,#fff,#333);
            border-radius: 50%;
            margin:10px auto;
            box-shadow:2px 2px 4px rgba(0,0,0,0.3);
            cursor:pointer;
        }
        .chess_white{
            background-color: #eeeeee;
            radial-gradient(15px 15px at 15px 15px,#fff,#e2e2e2);
        }

        .chess:after{
            content: "";
            display: block;
            width: 10px;
            height: 5px;
            border-radius: 50%;
            position: absolute;
            top: 5px;
            left: 2px;
            transform: rotate(-45deg);
            background: radial-gradient(10px 5px at 5px 2px,#fff,#aaa);
            box-shadow: 0 0 8px #fff;
        }

        .chess_white:after{
            transform: rotate(-60deg);
            background: radial-gradient(20px 10px at 10px 5px,#fff,#cccc);
            box-shadow: 0 0 8px #fff;
        }
        .chess[draggable=false]:hover{

            cursor:not-allowed;
        }

        .chess_name{
            text-align: center;
        }



        /*棋盘*/
        article{padding:30px;}
        .chessboard{
            margin:0 auto;
            width:700px;
            height: 700px;
            background:url("./public/images/chessboard.jpg") center center no-repeat;
            background-size: contain;
            padding:22px;
        }
        .chessboard table{
            height: 100%;
        }

        .chessboard table td{
            width:40px;
            height:40px;
            /*border:1px dashed #f00;*/
        }
        .chessboard table td .chess{
            margin:0px auto;
        }



        p{
            text-align: center;
        }
        select{
            border:none;
            border:1px solid #eee;
            height: 25px;
            width:100px;
        }
        .now_step{
            padding:30px 10px;
        }
        .step_text{
            display: inline-block;
            height: 25px;
            line-height: 25px;
        }
        .step_color{
            display: inline-block;
            width:25px;
            height: 25px;
            background-color: #333333;
        }

    </style>

    <script>
        window.onload=function(){
            init();


            //判读当前步骤
            document.querySelector('#priority').oninput=function(){
                if(this.value==0){
                    document.querySelector('.step_color').style.backgroundColor='#333';
                    document.querySelector('.white_box .chess').setAttribute('draggable','false');
                    document.querySelector('.black_box .chess').setAttribute('draggable','true');
                }else{
                    document.querySelector('.step_color').style.backgroundColor='#fff';
                    document.querySelector('.black_box .chess').setAttribute('draggable','false');
                    document.querySelector('.white_box .chess').setAttribute('draggable','true');
                }

            }

            // 实现拖拽步骤
            var chesses = document.querySelectorAll('.chess_box .chess');
            var target_boxs = document.querySelectorAll('td');

            // 第一步实现拖拽
            chesses.forEach(item=>{
                item.ondragstart = function(e){
                    var html= e.target.outerHTML;
                    e.dataTransfer.setData('text/html',html);
                }
                item.ondrag = function(e){

                }
                item.ondragleave = function(e){
                    console.log('ondrapleave');
                }
                item.ondragend = function(e){

                }
            })


            //棋盘接收
            target_boxs.forEach(item=>{
                //拖拽接收位置
                item.ondrogenter = function(e){

                }

                //注意 实现拖拽，在ondrapover时必须阻止默认行为
                item.ondragover = function(e){
                    e.preventDefault();

                }

                //拖拽目标位置松开鼠标
                item.ondrop = function(e){
                    //锁死下棋优先设置选择
                    document.querySelector('#priority').setAttribute('disabled',true);

                    var html = e.dataTransfer.getData('text/html');
                    //判读是否为白棋
                    if(html.includes('chess_white')){
                        document.querySelector('.step_color').style.backgroundColor='#333';
                        document.querySelector('.black_box .chess').setAttribute('draggable','true');
                        document.querySelector('.white_box .chess').setAttribute('draggable','false');
                    }else{
                        document.querySelector('.step_color').style.backgroundColor='#fff';
                        document.querySelector('.black_box .chess').setAttribute('draggable','false');
                        document.querySelector('.white_box .chess').setAttribute('draggable','true');
                    }

                    e.target.innerHTML=html;

                    //去除draggable属性
                    document.querySelectorAll('td .chess').forEach(item=>{
                        item.setAttribute('draggable','false');
                    })
                }

                item.ondragleave = function(e){

                }
            })

        }

        window.onresize = function(){
            init();
        }

        //初始化主要显示区域高度
        function init(){
            var height=window.innerHeight;
            height = height>970?height:970;
            document.querySelector('aside').style.height=(height-200)+'px';
            document.querySelector('article').style.height=(height-200)+'px';
        }
    </script>
</head>
<body>
<header>
    <h3>五子棋</h3>
</header>
<main>
    <aside>
        <div class="chess_box black_box">
            <div class="chess" draggable="true"></div>
            <div class="chess_name">黑棋</div>
        </div>
        <div class="chess_box white_box">
            <div class="chess chess_white" draggable="false"></div>
            <div class="chess_name">白棋</div>
        </div>
        <div>
            <p>
                <select id="priority">
                    <option value="0">黑棋先走</option>
                    <option value="1">白棋先走</option>
                </select>
            </p>
        </div>
        <div class="now_step">
            <span class="step_text">当前：</span>
            <span class="step_color"></span>
        </div>
    </aside>
    <article>
        <div class="chessboard">
            <table  width="100%" border="0" cellspacing="0" cellpadding="0">
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
            </table>
        </div>
    </article>
</main>
<footer>
    <p>如非客 &copy;Copy rueike2019</p>
</footer>

</body>
</html>
```

##### 视频播放器组件案例

- 实现功能
  - 全屏切换
  - 进度条点击跳播
  - 音量点击设置大小

- 涉及知识点

  - video对象属性

    - .duration 获取视频总长度（秒）
    - .currentTime 当前播放时间（秒）
    - .volume 获取音量或设置音量 （值0-1)
    - .paused 是否暂停状态 （true/false)

  - video 对象方法

    - .play() 播放
    - .pause() 暂停

  - video 对象事件

    - .oncanplay 视频资源可以播放时触发

    - .ontimeupdate 视频播放过程中或时间更改时触发

    - .onended 视频播放完毕后

      

- 注意点

  - 进度条（音量控制条） 由3层div组成，控制层，当前时间层和总时长层，叠加在一起，最上层用来点击触发事件
  - 火狐上无法监控oncanplay()方法，暂无解决

   ![效果1](https://img-blog.csdnimg.cn/20191020230953498.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3J1ZmVpa2U=,size_16,color_FFFFFF,t_70) 

- 案例代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link href="//netdna.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css" rel="stylesheet">
    <title>自定义视频播放器</title>
    <style>
        *{box-sizing: border-box}
        .player{
            width:970px;
            height:670px;
            margin:0 auto;
            background-color: #222;
            padding:10px;
            -moz-user-select:none; /* Firefox私有属性 */
            -webkit-user-select:none; /* WebKit内核私有属性 */
            -ms-user-select:none; /* IE私有属性(IE10及以后) */
            -khtml-user-select:none; /* KHTML内核私有属性 */
            -o-user-select:none; /* Opera私有属性 */
            user-select:none; /* CSS3属性 */
        }
        .show{
            text-align: center;
            height: 600px;
            background: #333;
            background:url('./public/images/loading.gif') center center;
            background-size: contain;
        }
        video{
            display: none;
            width:auto;
            max-width: 100%;
        }

        .controller{
            color:#fff;
            padding:15px 0;
        }
        .controller_tool{
            float:left;
            text-align: center;
            cursor:pointer;
        }
        .player_btn{
            width:50px;
        }
        .pull_btn{
            float:right;
            width:50px;
        }
        .progress{
            height:6px;
            border-radius: 2px;
            margin-top:8px;
        }
        .total_progress{
            width:650px;
            background-color:#666;
        }
        .current_progress{
            position:absolute;
            width:0px;
            background-color:yellowgreen;
        }
        .bar{
            position:absolute;
            width:650px;
            z-index: 99;
        }
        .time_box{
            margin-left:15px;
            cursor:default;
        }
        .volume_box{
            position:relative;
            width:40px;
            padding:0 10px;
        }
        .volume_proress_now {
            border-radius: 4px;
            top:-30px;
            left:16px;
            position:absolute;
            width:6px;
            height:30px;
            background-color: yellowgreen;
        }
        .volume_proress{
            border-radius: 4px;
            top:-60px;
            left:16px;
            position:absolute;
            width:6px;
            height:60px;
            background-color: #666;
        }
        .volume_proress_bar{
            border-radius: 4px;
            top:-60px;
            left:16px;
            position:absolute;
            width:6px;
            height:60px;
        }
        .volume_bar_box{
            display: none;
        }
    </style>
</head>
<body>
<main>
    <div class="player">
        <div class="show">
            <video id="my_video" height="100%" src="./public/media/1.mp4"></video>
            <div class="loading"></div>
        </div>
        <div class="controller">
            <div class="controller_tool player_btn"><i class="fa fa-play" aria-hidden="true"></i></div>
            <div class="controller_tool player_progress">
                <div class="progress bar"></div>
                <div class="progress current_progress"></div>
                <div class="progress total_progress"></div>
            </div>
            <div class="controller_tool time_box">
                <span id="current_time">00:00:00</span>
                /
                <span id="total_time">00:00:00</span>
            </div>
            <div class="controller_tool volume_box">
                <div class="volume_bar_box">
                    <div class="volume_proress"></div>
                    <div class="volume_proress_now"></div>
                    <div class="volume_proress_bar"></div>
                </div>
                <i class="fa fa-volume-up" aria-hidden="true"></i>
            </div>
            <div class="controller_tool pull_btn"><i class="fa fa-arrows-alt" aria-hidden="true"></i></div>
        </div>
    </div>
</main>
<script>
    window.onload=function(){
        var video = document.querySelector('#my_video');
        //视频可以播放时，初始化控制面板上的数据
        video.oncanplay=function(){
            //默认为等待图标 显示视频内容
            video.style.display='inline-block';
            //设置默认音量
            video.volume = 0.5;
            //获取视频总时长
            var total_time=formatTime(video.duration);
            document.querySelector('#total_time').innerHTML=total_time;
        };

        //视频在播放过程中更改播放进度条
        video.ontimeupdate = function(){
            var current_time = video.currentTime;
            var total_time = video.duration;
            document.querySelector('#current_time').innerHTML=formatTime(current_time);
            //进度百分比
            var w=document.querySelector('.total_progress').clientWidth;
            document.querySelector('.current_progress').style.width=(current_time/total_time)*w+'px';
        }

        //播放完毕的时候，把播放时间回到初始位置
        video.onended = function(){
            video.currentTime = 0;
            document.querySelector('.player_btn i').classList.remove('fa-stop');
            document.querySelector('.player_btn i').classList.add('fa-play');
        }


        //点击进度条进行跳播
        document.querySelector('.bar').onclick=function(e){
            //获取总长度
            var w = this.clientWidth;
            //获取鼠标偏移量
            var c_w = e.offsetX;

            //根据偏移量获取总时间的百分比
            var now_time = video.duration * (c_w/w);
            video.currentTime = now_time;

        }

        //控制音量组件显示/隐藏
        document.querySelector('.fa-volume-up').onclick = function(e){
            if(this.classList.contains('active')){
                this.classList.remove('active');
                document.querySelector('.volume_bar_box').style.display='none';
            }else{
                this.classList.add('active');
                document.querySelector('.volume_bar_box').style.display='block';
            }

            //阻止冒泡事件
            e.stopPropagation();
            e.preventDefault();
        }

        //收起音量设置控制条
        document.onclick = function(){
            document.querySelector('.fa-volume-up').classList.remove('active');
            document.querySelector('.volume_bar_box').style.display='none';
        }

        //设置音量大小
        document.querySelector('.volume_proress_bar').onclick = function(e){
            var h = this.clientHeight;
            var c_h=h-e.offsetY;
            //设置音量
            video.volume = c_h/h;
            //设置对应的音量高度
            document.querySelector('.volume_proress_now').style.height=c_h+'px';
            document.querySelector('.volume_proress_now').style.top=-c_h+'px';
            e.stopPropagation();
            e.preventDefault();
        }

        // 点击播放时
        document.querySelector('.player_btn').onclick=function(){
            if(video.paused){
                video.play();
                document.querySelector('.player_btn i').classList.remove('fa-play');
                document.querySelector('.player_btn i').classList.add('fa-stop');
            }else{
                video.pause();
                document.querySelector('.player_btn i').classList.remove('fa-stop');
                document.querySelector('.player_btn i').classList.add('fa-play');
            }
        }

        //全屏切换
        document.querySelector('.pull_btn').onclick=function(){
            var player=document.querySelector('.player');
            var flag = document.fullscreenElement || document.webkitFullscreenElement ||document.mozFullScreenElement ||document.msFullscreenElement ||document.oFullscreenElement;

            if(flag){//全屏状态
                //兼容性问题
                if(document.cancelFullScreen){
                    document.cancelFullScreen();
                }else if(document.webkitCancelFullScreen){//chome
                    document.webkitCancelFullScreen();
                }else if(document.mozCancelFullScreen){//fox
                    document.mozCancelFullScreen();
                }else if(document.msCancelFullScreen){//ie
                    document.msCancelFullScreen();
                }else if(document.oCancelFullScreen){//opera
                    document.oCancelFullScreen();
                }

                //窗口大小设置
                document.querySelector('.show').style.height=600+'px';
                document.querySelector('.total_progress').style.width=650+'px';

                //切换图标
                document.querySelector('.pull_btn i').classList.remove('fa-compress');
                document.querySelector('.pull_btn i').classList.add('fa-arrows-alt');
            }else{
                //兼容性问题
                if(player.requestFullScreen){
                    player.requestFullscreen();
                }else if(player.webkitRequestFullScreen){//chome
                    player.webkitRequestFullScreen();
                }else if(player.mozRequestFullScreen){//fox
                    player.mozRequestFullScreen();
                }else if(player.msRequestFullScreen){//ie
                    player.msRequestFullScreen();
                }else if(player.oRequestFullScreen){//opera
                    player.oRequestFullScreen();
                }
                //窗口大小设置
                document.querySelector('.show').style.height=window.outerHeight-40+'px';
                document.querySelector('.total_progress').style.width=window.innerWidth-350+'px';
                //切换图标
                document.querySelector('.pull_btn i').classList.remove('fa-arrows-alt');
                document.querySelector('.pull_btn i').classList.add('fa-compress');
            }
        }

        //解决esc或h5全屏自带的退出无法恢复原大小问题
        window.onresize=function() {
            var flag = document.fullscreenElement || document.webkitFullscreenElement ||document.mozFullScreenElement ||document.msFullscreenElement ||document.oFullscreenElement;
            if (!flag) {
                //窗口大小设置
                document.querySelector('.show').style.height=600+'px';
                document.querySelector('.total_progress').style.width=650+'px';

                //切换图标
                document.querySelector('.pull_btn i').classList.remove('fa-compress');
                document.querySelector('.pull_btn i').classList.add('fa-arrows-alt');
            }
        }
    }



    //时间格式化 参数-秒
    function formatTime(time){
        if(typeof(time)!=="number"){
            return '00:00:00';
        }

        //获取hour
        var hour=parseInt(time/(60*60));
        hour = hour<10?'0'+hour:hour;

        //获取分钟
        var minute=parseInt(time%(60*60)/60);
        minute = minute<10?'0'+minute:minute;

        //获取秒钟
        var second=Math.ceil(time%60);
        second = second<10?'0'+second:second;

        return `${hour}:${minute}:${second}`;
    }
</script>
</body>
</html>

```





## css3

