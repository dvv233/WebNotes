## **html/css 笔记**
**1. 行内元素和块状元素**
- 块状元素：div h dt dd li p...块级元素总是从新的一行开始，即各个块级元素独占一行，默认垂直向下排列；高度、宽度、margin及padding都是可控的，设置有效，有边距效果；宽度没有设置时，默认为100%。
- 行内元素：a b span i input img...行内元素和其他元素都在一行，即行内元素和其他行内元素都会在一条水平线上排列；高度、宽度是不可控的，设置无效，由内容决定。

**2. 伪类和伪元素：**
> 区别：是否创建列新元素。
- 伪类：用于已有元素处于某种状态时为其添加对应的样式，这个状态是根据用户行为而动态变化的。例如：当用户悬停在指定元素时，可以通过:hover来描述这个元素的状态，虽然它和一般css相似，可以为 已有元素添加样式，但是它只有处于DOM树无法描述的状态下才能为元素添加样式，所以称为伪类。
- 伪元素：用于创建一些不在DOM树中的元素，并为其添加样式。例如，我们可以通过:before来在一个元素之前添加一些文本，并为这些文本添加样式，虽然用户可以看见 这些文本，但是它实际上并不在DOM文档中。

**3. html语义标签**
> HTML5中加入了一些语义化标签，来更清晰的表达文档结构。如 title、header、nav、article、section、aside、footer、 strong等。语义化更具有可读性，代码更好维护。

**4. h5新增特性**
- 媒体播放的video 和 audio
``` css
<video src=# poster="" preload = auto/meta/none loop controls muted></video>
<!-- cobtrols是设置是否有播放的组件
muted默认静音
Poster设置视频封面 -->
<audio duration  paused  volume  starttime   currentTime.....></audio>
```

**5. 选择器类型**
> !important    内联样式（1000）    ID选择器（0100）    类选择器/属性选择器/伪类选择器（0010）(相等优先级)      元素选择器/伪元素选择器（0001）
关系选择器/通配符选择器（0000）
【带!important 标记的样式属性优先级最高； 样式表的来源相同时：!important > 行内样式>ID选择器 > 类选择器 > 标签 > 通配符 > 继承 > 浏览器默认属性】

**6. position属性**
- 固定定位 fixed： 元素的位置相对于浏览器窗口是固定位置，即使窗口是滚动的它也不会移动。Fixed 定位使元素的位置与文档流无关，因此不占据空间。 Fixed 定位的元素和其他元素重叠。
- 相对定位 relative： 如果对一个元素进行相对定位，它将出现在它所在的位置上。然后，可以通过设置垂直或水平位置，让这个元素“相对于”它自己的起点进行移动（↓→为正）在使用相对定位时，无论是否进行移动，元素仍然占据原来的空间，不会脱离文档流和改变元素性质。【灵魂出窍】
- 绝对定位 absolute： 绝对定位的元素的位置相对于最近的已定位父元素，如果元素没有已定位的父元素，那么它的位置相对于absolute 定位使元素的位置与文档流无关，因此不占据空间。 absolute 定位的元素和其他元素重叠，定位元素提升一个层级覆盖其他元素。【层级特点：父子水涨船高；同级后者居上。】
- 粘性定位 sticky： 元素先按照普通文档流定位，然后相对于该元素在流中的 flow root（BFC）和 containing block（最近的块级祖先元素）定位。而后，元素定位表现为在跨越特定阈值前为相对定位，之后为固定定位。
- 默认定位 Static： 默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声 明）。 inherit: 规定应该从父元素继承 position 属性的值。

**7. 让一个元素水平垂直居中**
+ 水平居中
    - 对于行内元素 : text-align: center;
    - 对于确定宽度的块级元素：
        * width和margin实现。margin: 0 auto;
        * 绝对定位和margin-left: -width/2, 前提是父元素position: relative
    - 对于宽度未知的块级元素
        * table标签配合margin左右auto实现水平居中。使用table标签（或直接将块级元素设值为 display:table），再通过给该标签添加左右margin为auto。
        * inline-block实现水平居中方法。display：inline-block和text-align:center实现水平居中。
        * 绝对定位+transform，translateX可以移动本身元素的50%。
        * flex布局使用justify-content:center
+ 垂直居中
    - 利用 line-height 实现居中，这种方法适合纯文字类。
    - 通过设置父容器 相对定位 ，子级设置 绝对定位，标签通过margin实现自适应居中。
    - 弹性布局 flex :父级设置display: flex; 子级设置margin为auto实现自适应居中。
    - 父级设置相对定位，子级设置绝对定位，并且通过位移 transform 实现。
    - table 布局，父级通过转换成表格形式，然后子级设置 vertical-align 实现。（需要注意的是：vertical-align: middle使用的前提条件是内联元素以及display值为table-cell的元素）

**8. 脱离文档流**
> 块元素变成行内块元素，宽高由内容撑开，也可自己设置。

**9. 浮动的特点**
+ 浮动的特点：
    - 浮动在父元素范围内，不会从父元素中移出。
    - 元素设置浮动后，会完全从文档流中脱离，不再占用文档流的位置。之后的元素会自动向上移动占用文档流的位置。
    - 浮动元素不会超过前面的浮动元素，利用此特点可以设置水平排列布局。
    - 浮动元素不会超过前面的浮动元素，利用此特点可以设置水平排列布局。
+ 清除浮动的方法：
    - 伪元素清除浮动：给浮动元素父级增加
    ```css
    clearfix::after { content: ''; display: table; clear: both; } /*兼容IE低版本 是当下清除浮动最流行的方法。*/
    ```
    - 给浮动元素父级增加`overflow：hidden`属性。不会新增标签，但是如果父级元素有定位元素超出父级，超出部分会隐藏，在不涉及父级元素有超出内容的情况，`overflow：hidden`比较常用。
    - 额外标签法：给浮动元素父级增加标签。
    
**10. BFC** 
> BFC(Block Formatting Context)块级格式化上下文，是Web页面一块独立的渲染区域，内部元素的渲染不会影响边界以外的元素。 BFC布局规则 内部盒子会在垂直方向，一个接一个地放置。 Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠。 每个盒子（块盒与行盒）的margin box的左边，与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。 BFC的区域不会与float box重叠。 BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。 计算BFC的高度时，浮动元素也参与计算。 
+ BFC形成的条件 
    - `float `设置成 `left `或 `right` ,不为none ;
    - 绝对元素定位`position `是`absolute`或者`fixed`
    - `overflow `不是`visible`，为 `auto`、`scroll`、`hidden` 
    - 行内块和弹性盒`display`是`flex`或者`inline-block` 等 。
