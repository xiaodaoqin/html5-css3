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

#### radio 音频 

#### video 视频

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

### 获取DOM元素

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



## css3