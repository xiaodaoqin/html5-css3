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

### 新增表单type属性

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

### 新增表单其他属性

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

### 表单新增属性datalist

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



## css3