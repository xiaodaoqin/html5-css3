# CSS3学习笔记


## 选择器

### 属性选择器

- E[attr] 表示存在attr属性即可

  ```html
  div[class]
  ```

  

- E[attr=val] 表示属性值完全等于val;

  ```html
  div[class=myClass]
  ```

  

- E[attr*=val] 表示属性值中包含val字符，任意位置

  ```html
  div[class=myClass]
  ```

  

- E[attr^=val] 表示属性值中包含与val字符开头的

  ```html
  div[class=myClass]
  ```

  

- E[attr$=val] 表示属性值中包含与val字符结尾的

  ```html
  div[class=myClass]
  ```

  

### 伪类选择器

#### 兄弟伪类

- +：获取当前元素的相邻的满足条件的元素

- ~：获取当前元素的满足条件的兄弟元素

  ```html
  //只有.first相邻且为li标签元素被选
  .first+li{
  	color:red;
  }
  
  //其父级元素内符合条件的li元素都会被选择
  .first~li{
  	color:blue;
  }
  
  <ul>
      <li class="first">前端与移动开发</li>
      <li>javascript</li>
      <li>java</li>
      <li>php</li>
      <li>c++</li>
  </ul>
  
  
  ```

  

#### 结构伪类

与某元素相对与其父元素或兄弟元素的位置来获取元素(不关心类型)

- E:first-child：查找E这个元素的父元素第一个子元素E
- E:last-child：查找E这个元素的父元素最后一个子元素E
- E:nth-child(n)：查找E这个元素的父元素中第n个子元素E(注意：n是由1开始)
- E:nth-last-child(n)：查找E这个元素的父元素倒数第n个子元素E
- E:nth-child(even)：查找E这个元素的父元素所有偶数子元素E
- E:nth-child(odd)：查找E这个元素的父元素所有奇数子元素E
- E:empty：选择没有认字子节点的E元素，注意：空格也算子元素

```html
<style>
    list:first-child{
        color:red;
    }
</style>
<ul>
    <span>我不会被过滤掉</span>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
    <li>6</li>
    <li>7</li>
    <li>8</li>
</ul>
```

上面代码：由于span标签处于第一位，所有第一个li不会被选择





与某元素相对与其父元素或兄弟元素的位置来获取元素(限制类型)

- E:first-of-type：查找E这个元素的父元素第一个子元素E
- E:last-of-type：查找E这个元素的父元素最后一个子元素E
- E:nth-of-type(n)：查找E这个元素的父元素中第n个子元素E(注意：n是由1开始)
- E:nth-of-type(n)：查找E这个元素的父元素倒数第n个子元素E
- E:nth-of-type(even)：查找E这个元素的父元素所有偶数子元素E
- E:nth--of-type(odd)：查找E这个元素的父元素所有奇数子元素E

```html
<style>
    list:first-of-type{
        color:red;
    }
</style>
<ul>
    <span>我会被过滤掉</span>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
    <li>6</li>
    <li>7</li>
    <li>8</li>
</ul>
```

上面代码：第一个li标签会被选择



#### target伪类颜色

E:target：可以为锚点目标元素添加样式，当目标元素被触发为当前锚点链接的目标是，调用此伪类样式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        li{
            list-style: none;
        }
        aside{
            float:left;
            width:120px;
        }

        article{
            margin-left:120px;
        }

        p:first-child{
            font-size:20px;
            font-weight: 700;
        }
        p:last-child{
            text-indent: 2em;
            line-height: 25px;
            letter-spacing:3px;
            padding:0 0 100px 0;
        }

        #nav_list{
            position:fixed;
        }

        p:target{
            color:#ff0000;
        }
    </style>
</head>
<body>
    <main>
        <aside>
            <ul id="nav_list">
                <li><a href="#javascript">javascript</a></li>
                <li><a href="#php">php</a></li>
                <li><a href="#java">java</a></li>
                <li><a href="#c++">c++</a></li>
            </ul>
        </aside>
        <article>
            <ul>
                <li>
                    <p id="javascript">javascript</p>
                    <p>
                        javascript为web前端开发必须掌握技能，可以操控页面内的元素DOM节点，从而达到为所欲为的效果
                        javascript为web前端开发必须掌握技能，可以操控页面内的元素DOM节点，从而达到为所欲为的效果
                        javascript为web前端开发必须掌握技能，可以操控页面内的元素DOM节点，从而达到为所欲为的效果
                        
                   </p>
                </li>
                <li>
                    <p id="php">php</p>
                    <p>
                        php是世界上最好的语言，毋庸置疑！！！！！
                        php是世界上最好的语言，毋庸置疑！！！！！
                        php是世界上最好的语言，毋庸置疑！！！！！
                        php是世界上最好的语言，毋庸置疑！！！！！
                        
                       
                    </p>
                </li>
                <li>
                    <p id="java">java</p>
                    <p>
                        java可以做任何事情，是目前使用最广的编程语言
                        java可以做任何事情，是目前使用最广的编程语言
                        java可以做任何事情，是目前使用最广的编程语言
                        java可以做任何事情，是目前使用最广的编程语言
                       
                        
                    </p>
                </li>
                <li>
                    <p id="c++">c++</p>
                    <p>
                        c++是C语言的加强版，主要应用与桌面应用程序。
                        c++是C语言的加强版，主要应用与桌面应用程序。
                        c++是C语言的加强版，主要应用与桌面应用程序。
                        c++是C语言的加强版，主要应用与桌面应用程序。
                        c++是C语言的加强版，主要应用与桌面应用程序。
                                                
                    </p>
                </li>
            </ul>
        </article>
    </main>
</body>
</html>
```



## 伪元素before 、after

- <div style="color:red">重点：`E::before`、`E::after`</div>
- 是一个行内元素，如果还需要设置宽高，需要设置display、position、float
  - 必须增加content属性，不管是否设置内容，`content:""`
  - 旧版写法`E:before`、`E:after` ，新版写法：`E::before`和`E::after`。
  - IE8或IE8前的版本，不支持

## 其他伪元素

- E::first-letter：文本的第一个字母或字
- E::first-line：文本第一行
- E::selection：可以改变选中文本的样式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        /*通过E::first-letter实现首字下沉*/
        p::first-letter{
            color:red;
            font-size:30px;
            float:left;/*文本环绕*/
        }


        /*
            E::获取第一行内容，设置其样式，注意其他伪类选择内容不参与
        */
        p::first-line{
            font-size:25px;
            font-style: italic;
        }

        /*
            E::selection设置选择内容的样式
         */
        p::selection{
            color:#aaaaaa;
        }

    </style>
</head>
<body>
    <p>眉毛上的汗水和眉毛下的泪水，你必须选择一样<br>你不能努力，活该生活在社会的最底层</p>
</body>
</html>

```



## 颜色设置

- 直接使用语义单词或#FF00FF
- rgb和rgba
  - rgb(255,128,255)
  - rgba(255,122,266,0.6)

- hsl和hsla
  - H:Hue(色调，色相)，0-360 过度，0或360为红色 （红、橙、黄、绿、青、蓝、紫、红）
  - S:Saturation(饱和度) 取值范围：0.0%~100.0%
  - L:Lightness(亮度）取值范围 0.00%~100.0%，50%是平衡值
  - A:Alpha(透明度) 取值 0~1之间
  - 语法：hsla(120,10%,50%,0.5)

## 文件阴影

- 语法： text-shadow:<X轴偏移量> <Y轴偏移量> <模糊程度> <颜色> 如：`text-shadow:2px 3px 2px #000;`

- 可以加多次阴影 ，使用`,`隔开 如：text-shadow:2px 2px 2px  #f0f,3px 3px 2px 0;

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        main{
            width:300px;
            margin:0 auto;
        }
        
        main div{
            background: #999999;
            color:#ffffff;
            text-align: center;
            margin-bottom: 15px;
            line-height: 100px;
            font-size:25px;
            font-weight: 700;
            letter-spacing: 2px;
        }

        /*
            text-shadow:offsetX offsetY blur color;
         */

        .demo1 {
            text-shadow: -1px -1px 5px #ff0000;
        }

        .demo2{
            text-shadow: 0px 0px 10px #ffffff;
        }

        /*多层阴影*/
        .demo3{
            text-shadow:2px 2px 5px #ff0000,3px 3px 5px #ff00ff;
        }

        /*多层阴影*/
        .demo4{
            color:#000000;
            text-shadow:-1px -1px 0px #eee,-2px -2px 0px #ddd,-3px -3px 0px #ccc;
        }


    </style>
</head>
<body>
    <main>
        <div class="demo demo1">CSS3入门教程</div>
        <div class="demo demo2">CSS3入门教程</div>
        <div class="demo demo3">CSS3入门教程</div>
        <div class="demo demo4">CSS3入门教程</div>
    </main>
</body>
</html>
```

### 盒子模型

- box-sizing:border-box; 盒子总宽高：边框+内边距+内容
- box-sizing: content-box;盒子总宽高：内容

## 圆角

- box-radius :<左上角> <右上角> <右下角> <左下角> 
- box-radius后面只给一个值时，等于4个交都是按该值画圆角 
- box-radius后面2个值时，对角设置
- box-radius后面3个值时，右上角和左下角公用中间值

## 安卓图标案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .icon_box{width:300px;height: 300px;margin:0 auto;border:1px solid #ececec;padding:10px;}
        .an_header{position:relative;width:100px;height: 50px;margin:0 auto;background-color: darkgreen;border-radius: 100px 100px 0 0;margin-bottom: 5px;}
        .an_header::before,.an_header::after{
            content:'';
            background-color: #ffffff;
            position: absolute;
            top:25px;
            width:10px;
            height: 10px;
            border-radius: 50%;
        }
        .an_header::before{left:26px;}
        .an_header::after{right:26px;}
        .an_body{position:relative;width:100px;height: 100px;background-color: darkgreen;margin:0px auto;border-radius: 0 0 10px 10px;}
        .an_body::before,.an_body::after{
            content:'';
            position: absolute;
            width:15px;
            height: 70px;
            top:10px;
            background: darkgreen;
            border-radius: 5px;
        }
        .an_body::before{left:-20px}
        .an_body::after{right:-20px}
        .an_footer{position:relative;width:100px;height: 100px;background-color: #ffffff;margin:0px auto;border-radius: 0 0 10px 10px;}
        .an_footer::before,.an_footer::after{
            content:'';
            position: absolute;
            width:15px;
            height: 70px;
            background: darkgreen;
            border-radius:0px 0px 5px 5px;
        }
        .an_footer::before{left:20px}
        .an_footer::after{right:20px}
    </style>
</head>
<body>
    <main>
        <div class="icon_box">
            <div class="an_header"></div>
            <div class="an_body"></div>
            <div class="an_footer"></div>
        </div>
    </main>
</body>
</html>


```



## 渐变

### 线性渐变

- linear-gradient([<point>||<angle>,]?<stop>,<stop>[,<stop>]*)
- 参数说明：
  - 第一个参数表示线性渐变的方向
    - to left：设置渐变为从右到左，相当于 270deg；
    - to right：从左到右，相当于90deg;
    - to top：从下到上，相当于0deg;
    - to bottom：从上到下，相当与180deg 为默认值
  - 第二个参数：起点颜色，可以指定颜色位置
  - 第三个参数：终点颜色
  - 还可以增加多个参数，表示多种颜色的渐变

### 径向渐变

- radial-gradient(<形状>,开始颜色，结束颜色) 如：background:radial-gradient(circle,red,blue)
- 参数说明：
  - 第一个参数可以写circle和ellipse，circle只能产生正方形渐变，ellipse可以根据现状进行渐变

## 背景属性

- 添加背景颜色 ：background-color:skyblue
- 添加背景图片：background-image:url('../images/i.jpg')
- 设置背景平铺：background-repeat:no-space
  - round 会把图片进行缩放后再进行平铺
  - space 图片不缩放平铺
  - on-space 不平铺，只有一个

- 设置在滚动容器的背景行为：background-attachment:fixed;
  - fixed：背景图片位置固定不变，不会跟随内容滚动
  - scroll：背景跟随滚动
  - local：与fixed区别，与背景内容一起滚动。

- 设置背景图片的大小：background-size:cover;
  - <span style="color:red">cover</span>：放大铺满
  - <span style="color:red">contain</span>：缩小铺满
  - auto：原始图片大小
  - <span style="color:red">number</span>（直接写数值）
  - percentage(百分比)

- 设置背景偏移：background-position:-20px 0;

  - 该偏移参照background-origin原定，这个原点默认在容器左上角

- 设置背景坐标原点：background-origin:padding-box;

  - border-box：从border的位置开始填充背景，会与border重叠
  - padding-box：从padding的位置开始填充背景，会与padding重叠
  - content-box：从content的位置开始填充背景，会与content重叠
  -  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191021232325316.png) 

    

- 设置内容裁切：background-clip:border-box;

  - border-box：从border的位置开始显示内容

     ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191022003247887.png) 

  - padding-box：从padding的位置开始显示内容

     ![在这里插入图片描述](https://img-blog.csdnimg.cn/201910220034134.png) 

  - content-box：从content的位置开始显示内容

     ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191022003427213.png) 



## 边框图片

- 原理：九宫格填充

  <img src="E:\web\html+css3\笔记\images\2322.png" alt="2322" style="zoom: 50%;" />

- 插入边框图片： `border-image-source:url("../image/1.jpg")`

- 设置4个方向的的裁切 距离：`border-image-slice:27 fill;` 274个方向代表裁切距离 fill代表填充内容为位置

  <img src="E:\web\html+css3\笔记\images\QQ图片20191022093806.png" alt="QQ图片20191022093806" style="zoom: 25%;" />

- 设置边框图片的宽度：`border-image-width:27px;`,注意：设置边框图片宽度时，应与边框一致，避免边框图片溢出现象

  <img src="E:\web\html+css3\笔记\images\QQ图片20191022093917.png" alt="QQ图片20191022093917" style="zoom:25%;" />

- 设置边框拓展：`border-image-outset:0px;`，一般不使用

- 边框图片平铺：`border-image-repeat:repeat;`

  - repeat：直接平铺
  - round：缩小平铺，显示完整内容

  <img src="E:\web\html+css3\笔记\images\QQ图片20191022094312.png" alt="QQ图片20191022094312" style="zoom:50%;" />

- 缩写：`border-image:source slice /width/outset repeat;`
  
  - border-image:url("../image/1.jpg")  27 / 27px /0px round



- 边框图片-实现聊天背景案例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <style>
          .border{
              width:300px;
              height:auto;
              border:10px solid #ffffff;
              border-image-slice: 10 fill;
              border-image-width: 10px;
              border-image-source:url("./public/images/border.png");
          }
          .border2{
              border-image-repeat: repeat;
          }
          .border3{
              border-image-repeat: round;
          }
      </style>
  </head>
  <body>
      <div class="border">我要测试边框图片,我要测试边框图片,我要测试边框图片</div>
      <div class="border border2">我要测试边框图片,我要测试边框图片,我要测试边框图片</div>
      <div class="border border3">我要测试边框图片,我要测试边框图片,我要测试边框图片</div>
  </body>
  </html>
  ```

  

## 过渡动画

- 简写语法：`transition:property duration timing-function delay;`或按以下属性单独设置
  - transition-property：规定设置过渡效果的css属性名称
  - transition-duration：规定完成过度效果需要多少秒
  - transition-timing-function：规定速度效果的速度曲线
    - linear：规定以相同速度开始至结束的过渡效果，等同cubic-bezier(0,0,1,1)
    - ease：规定慢速开始，然后变快，然后慢速结束的过渡效果，等同cubice-bezier（0.25,0.1,0.25,1)
    - ease-in：规定以慢速开始的过渡效果，等同cubic-bezier（0.42,0,1,1）
    - ease-out：规定以慢速结束的过渡效果，等同cubice-bezier(0,0,0.58,1)
    - ease-in-out：规定以慢速开始和结束的过渡效果，等同cubic-bezier(0.42,0,0.58,1)
    - cubic-bezier(n,n,n,n)：在cubic-bezier函数中自定义自，可取范围0-1
  - transition-delay：定义过渡效果何时开始，单位秒
  - transition:all 2s steps(4); steps(n)指定过渡效果分几步完成
- 过渡效果兼容性问题：不同浏览器需要增加不同前缀处理
  - -moz-transition:all 2s steps(4);
  - -webkit-transition:all 2s steps(4);
  - -o-transition:all 2s steps(4);
  - transition:all 2s steps(4);
- 过渡效果只能应用在具体值的变化，不能应用状体值中，如：display

示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{
            margin:0;
            padding:0;
        }
        div{
            width:200px;
            height:200px;
            background-color: red;
            position:absolute;
            left:100px;
            top:100px;
            /*过渡属性*/
            /*transition-property: left;*/
            /*过渡时间*/
            /*transition-duration: 2s;*/
            /*过渡效果*/
            /*transition-timing-function: linear;*/
            /*过渡延时*/
            /*transition-delay: 0.3s;*/

            /*简写*/
            transition:left 2s linear 0.3s;

            /*多个过渡效果*/
            transition:left 2s linear 0.3s,background-color 2s linear 0.3s;

            /*所用过渡效果时间设置 不推荐使用，效率差*/
            /*transition:all 2s;*/

        }
        div:active{
            left:1000px;
            background-color: blue;
        }
    </style>
</head>
<body>
    <div></div>
    <script>

    </script>
</body>
</html>
```



手风琴菜单效果

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        * {
            padding: 0;
            margin: 0
        }

        main {
            width: 120px;
            margin: 30px auto;
        }

        li {
            list-style: none;
        }

        h3 {
            background-color: #cccccc;
            padding: 0 10px;
            line-height: 30px;
            border-bottom: 2px solid #bbbbbb
        }

        .sub_item_box>ul{
            background-color: #ececec;
            padding: 10px;
        }

        .sub_item_box{
            overflow:hidden;
            height: 0px;
            transition-property: height;
            transition-duration: 0.5s;

        }

        .item_box>li:hover .sub_item_box{
            height: 100px;
        }

        .sub_item_box li {
            line-height: 20px;
            border-bottom: 1px solid #cecece;
        }
    </style>
</head>
<body>
<main>
    <ul class="item_box">
        <li>
            <h3>主菜单一</h3>
            <div class="sub_item_box">
                <ul>
                    <li>子菜单1</li>
                    <li>子菜单2</li>
                    <li>子菜单3</li>
                    <li>子菜单4</li>
                </ul>
            </div>
        </li>
        <li>
            <h3>主菜单二</h3>
            <div class="sub_item_box">
                <ul>
                    <li>子菜单1</li>
                    <li>子菜单2</li>
                    <li>子菜单3</li>
                    <li>子菜单4</li>
                </ul>
            </div>
        </li>
        <li>
            <h3>主菜单三</h3>
            <div class="sub_item_box">
                <ul>
                    <li>子菜单1</li>
                    <li>子菜单2</li>
                    <li>子菜单3</li>
                    <li>子菜单4</li>
                </ul>
            </div>
        </li>
        <li>
            <h3>主菜单四</h3>
            <div class="sub_item_box">
                <ul>
                    <li>子菜单1</li>
                    <li>子菜单2</li>
                    <li>子菜单3</li>
                    <li>子菜单4</li>
                </ul>
            </div>
        </li>
    </ul>

</main>
</body>
</html>

```



## 2D转换过渡效果

### transform 移动

- 语法：`transform:translate(tx) | translate(tx,ty)`

  - tx代表x轴（横坐标）移动方向的长度，当其值为正值时，元素向x轴右方向移动，反之，元素向x轴左方向移动
  - ty代表y轴（纵坐标）移动方向的长度，当其值为正值时，元素向y轴<span style="color:red">下方</span>向移动，反之，元素向y轴<span style="color:red">上方</span>向移动。ty参数没有设置时，相当于ty=0
  - 可以单独使用`translateX(tx)`或 `translateY(ty)`

  示例1

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <style>
          * {
              padding: 0;
              margin: 0
          }
  
          div {
              width: 100px;
              height: 100px;
              background-color: #ff0000;
              /*增加过渡效果*/
              transition:transform 2s;
          }
  
          div:active {
              /*
              使用transform可以实现元素移动
              移动参照：左上角
              执行完毕后会恢复原始状态
               */
              /*向右移动 100px*/
              /*transform:translate(100px);*/
  
              transform:translate(200px,200px);
          }
      </style>
  </head>
  <body>
      <main>
          <div></div>
      </main>
  </body>
  </html>
  ```

  

### transform 缩放

- 定义：scale()让元素根据中心原点对象进行缩放，默认的值为1，因此0.01到0.99之间任意值，使一个元素缩小；而任意大于1的值，都会元素变得更大

- 语法：`transform:scale(sx|ty) | scale(sx,sy)`
- sx：指定x轴（横向坐标）方向的缩放向量，如果值为0.01~0.99之间，会使元素在x轴方向缩小，如果大于1，则放大
- sy：指定y轴（纵向坐标）方向的缩放向量，如果值为0.01~0.99之间，会使元素在y轴方向缩小，如果大于1，则放大
- 单独使用scaleX(sx)或scaleY(sy)



示例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        * {
            padding: 0;
            margin: 0
        }

        div {
            width: 100px;
            height: 100px;
            background-color: #ff0000;
            /*增加过渡效果*/
            transition:transform 2s;
            margin-bottom: 10px;
        }  
        /*缩放*/
        div:nth-of-type(2):hover{
            transform:scale(1.1);

        }
    </style>
</head>
<body>
    <main>
        <div></div>
        <div></div>
    </main>
</body>
</html>
```



### transform 旋转

- 定义：rotate()通过指定角度参数让元素根据中心原点对象进行旋转，正值时，顺时针转；负值时，逆时针旋转

- 语法：`transform:rotate(a)`

- a 代表旋转角度

- 单独使用rotateX(a),rotateY(a)

  

### transorm 斜切

- 定义：skew() 能够让元素倾斜希显示。他把可以把一个元素与中心位置围绕着x轴和y轴按照一定的角度倾斜；

- 语法：`transform:skew(a)`
- 单独使用 skewX(a),skewY(a)

### 设置旋转轴心

- ### `transform-origin:left`;默认值有left top right bottom center

### 同时添加多个属性

- transform:translateX(700px) rotate(-90 deg);
- 注意：旋转的时候会旋转坐标轴，因此都先移动，再旋转

### 实现任意元素居中

- 方式一：position定位和margin边距实现，该方式受定位元素大小影响，不同宽高的元素，需要计算margin的值。
- 方式二：position定位+transform:translate(-50%,-50%)移动实现，推荐使用，无需考虑定位元素的宽和高

代码示例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .container{position:relative;height: 200px;background-color: #cccccc;margin-bottom: 15px;}
        .circle{width:100px;height:100px;background-color: skyblue}
        .circle1{position:absolute;top:50%;left:50%;margin-top:-50px;margin-left:-50px;}
        .circle2{position:absolute;top:50%;left:50%;transform:translate(-50%,-50%)}
    </style>
</head>
<body>
    <p>方式一：position定位和margin边距实现</p>
    <div class="container">
        <div class="circle circle1"></div>
    </div>
    <p>方式二：position定位+transform:translate(-50%,-50%)移动实现</p>
    <div class="container">
        <div class="circle circle2"></div>
    </div>
</body>
</body>
</body>
</html>

```

## 3D转换过渡

三维变化使用基于二维变换的相同属性，同样使用transform属性进行设置

### 3D移动

- 方法：translate3d(x,y,z)
- 单独设置：translateX(length)，translateY(length)，translateZ(length)

### 3D缩放

- 方法：scale3d(x,y,z)
- 单独设置：scaleX(a)，scaleY(a)，scaleZ(a) 
- a取值范围0~1

### 3D旋转

- 方法：rotate3d(x,y,z,angle) 
  - x,y,z代表三个方向的偏移量
  - angle 旋转的角度

### 保留过渡结果

被转换的子元素保留其3d转换结果（需要设置在父元素中）

- transform-style:flat;子元素将不保留其3d位置-平面方式
- transform-style:preserve-3d;子元素将保留其3d位置 --立体方式

### 景深透视效果

- perspective:0px;
- perspective-origin:0px 0px; 透视观察角度

## 动画  

- 指定动画名称：animation-name: moveTest;

  - 定义动画

  ```html
  @keyframes moveTest {
              0% {
                  transform: translate(100px);
              }
              50% {
                  transform: translate(100px, 200px);
              }
              100% {
                  transform: translate(200px, 400px);
              }
          }
  ```

  

- 设置动画总耗时：animation-duration: 2s;

- 设置动画播放次数：animation-iteration-count: infinite; 默认为1次，可以指定数字，指定infinite为无限循环

- 设置动画交替执行：animation-direction: alternate; 从动画开始到结束，再倒过来执行

- 设置动画延时时间：animation-delay: 2s;

- 设置动画保留状态：animation-fill-mode: forwards;

- 设置动画时间函数：animation-timing-function: linear;匀速、变速

- 设置动画的播放状态 ：animation-play-state: running; paused 暂停 running 播放



示例代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: #ff0000
        }

        div {
            /*添加动画效果 */
            /*1.animation-name:指定动画名称 */
            animation-name: moveTest;
            /*2.animation-duration: 动画总耗时时间;*/
            animation-duration: 2s;
            /*3.animation-iteration-count: 动画播放次数; 默认为1次，可以指定数字，指定infinite为无限循环*/
            animation-iteration-count: infinite;
            /*animation-direction: alternate;设置交替动画*/
            animation-direction: alternate;
            /*animation-delay:2s 设置延时时间秒;*/
            animation-delay: 2s;

            /*animation-fill-mode: forwards|backwards|both;
               forwords:会保留动画结束时的状态
               backwords:不会保留动画结束时的状态；
               both:会保留动画结束时的状态
            设置动画结束时状态,动画结束时，默认会恢复原来状态*/
            animation-fill-mode: forwards;
            /*设置动画的时间函数*/
            animation-timing-function: linear;
            /*设置动画的播放状态 paused 暂停 running 播放*/
            animation-play-state: running;

        }

        @keyframes moveTest {
            0% {
                transform: translate(100px);
            }
            50% {
                transform: translate(100px, 200px);
            }
            100% {
                transform: translate(200px, 400px);
            }
        }
    </style>
</head>
<body>
<div></div>
</body>
</html>
```

