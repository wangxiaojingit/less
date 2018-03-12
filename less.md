### less

> less 是css 预编译语言.之所以用less,就是可以加快css书写速度,但是上线的时候,我们不用less,用的是less 转义之后的css.less只实用于开发环境.


less 编译工具 :`coala`

>   下载地址:http://koala-app.com/index-zh.html

> - 把less文件夹拖到koala工具中

> - 点击要转义的less文件,右键设置输出路径如:2.css.

> - 2.less写完之后,点击koala 工具中的执行编译即可.(输出模式一般选normal)
 
less 重点知识概括:

> - 1.注释,在less中支持//这也的注释.但是这种在转义之后不会在css中出现,要想出现,只有/*注释*/这种才可以.根据情况可以选择哪种注释.

> - 2.变量:@a:10px; 

> - 3.混合:

```css

@min:50px;
.box{width:@min;height:@min;background:green; .border1px}

.border1px{border:2px solid pink;}

  //混合传参,可以赋值默认值

.border_radius(@radiusdeg:10px){
    border-radius:@radiusdeg;
} 
.box{
    .border_radius()
} 
.box2{
    .box; //混合
    .border_radius(30px)
}

```
> - 匹配模式

```css
  // 匹配模式,根据传参的不同来匹配

.p(r){
    position:relative;
}
.p(f){
    position:fixed;
}
.p(a){
    position:absolute;
}

.box3{
    .box;
    .p(a) ;//参数传a 就是绝对定位

    .p(f); //参数产f 就是fixed定位

}
//接下来我们写一个稍微复杂点的匹配模式

//三角顶部朝上
.Triangle(top,@border-w:10px,@color:green){
     border-width:@border-w;
     border-color:transparent transparent @color transparent;
     border-style: dashed  dashed   solid dashed ;
}

//三角顶部朝下
.Triangle(bottom,@border-w:10px,@color:green){
    border-width:@border-w;
    border-color:@color transparent transparent  transparent;
    border-style:solid  dashed  dashed  dashed ;
}
//三角顶部朝左
.Triangle(left, @border-w, @color){
    border-width:@border-w;
    border-color:transparent @color transparent transparent;
    border-style:dashed  solid dashed  dashed ;
}

//三角顶部朝右
.Triangle(right,@border-w,@color){
  border-width:@border-w;
  border-color:transparent transparent transparent @color;
  border-style:dashed  dashed  dashed solid;
}
//这一部分是相当于公共部分.始终带着,其中第一个参数固定写法,后面的两个参数也必须带着.
.Triangle(@_,@border-w:50px,@color:green){
    width:0px;
    height:0px;
}
.mt200{margin-top:200px;}
.box4{
    .Triangle(top);
    width:0px;
    height:0px;
    .mt200;
}

```

> - less 可以嵌套,&表示上一级

```css

.box1{
    width:100px;
    height:100px;
    background:pink;
    &:hover{
      width:20px;
      height:20px;
      background:green;
    }
}


```

> - less 可以运算

```css

//less 可以运算
@a:20px;
.box{
    width:@a+20;
}
```
> @arguments 的用法

```css
//@arguments 的用法

.border(@w:1px,@style:solid,@color:green){
  // border:@w @style @color;
     border:@arguments

}
.box3{.border(20px)}

```
> - 避免编译 ~加双引号或者单引号

```css

.box3{
  width:~'calc(300px - 30px);' 
}

```
> - 增强优先级 !important

```css
.box4{
    .box1 !important;
}

```
