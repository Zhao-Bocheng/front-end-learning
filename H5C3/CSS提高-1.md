# CSS提高

## 转换（CSS3）

transform，是CSS3中具有颠覆性的特征之一，可以实现元素的位移、旋转、缩放等效果
**注意：转换属性对行内元素无效**

转换可以理解为变形

- 平移：translate
- 旋转：rotate
- 缩放：scale

### 转换原点

默认是在图形的中心

```css
transform-origin: x <y> <z>
/*默认值为 50% 50% 0*/
/*参数值可以为一个、两个或三个*/
/*一个值：取值为 length，percentage 或 left|center|right|top|bottom 中的一个*/
/*两个值：其中一个为 length，percentage或left|center|right 中的一个*/
/*另一个为 length，percentage或top|center|bottom 中的一个*/
/*三个值：前两个值和只有两个值时用法一致，而第三个值必须为 length（始终代表Z轴偏移量）*/
```

### 2D转换

2D转换的三种操作不会影响页面布局

#### 平移

CSS中移动盒子的方式主要有三种：定位、盒子外边距、2D平移

```css
transform: translate(x, <y>);	/* y不写则默认为 0 */
/* 或分开写 */
transform: translateX(n);
transform: translateY(n);
/* 上述参数的取值为 length 或 percentage */
/* percentage 是相对于元素自身尺寸的百分比。而不是相对于视窗尺寸的百分比*/
/* 2D平移操作不会影响到其他元素的布局，和相对定位的移动效果类似*/
```

#### 旋转

```css
transform: rotate(angle);
/* 参数取值为 angle —— 即 number + 单位deg，正值为顺时针，负值为逆时针 */
```

#### 缩放

```css
transform: scale(x, <y>) /*缺省 y ，则和 x 相同*/
/* 取值为 number ，如果缺省 y ，则默认值和 x 相同 */
/* 缩放量由矢量定义，矢量的坐标可定义在每个不同方向上各自己完成一定比例缩放
   当矢量的两个坐标 x, y 超出 [-1, 1] 范围外时，缩放将在坐标方向上放大元素
   当在 [-1, 1] 范围内时将在坐标方向上收缩元素
   特别的，当等于 1 时无任何变化，当为负时执行点反射和大小修改 */
```

#### 倾斜

在单个或多个方向上以一定角度扭曲元素上的每个点

```css
transform: skew(x, <y>)
/* x y 取值为 angle 当缺省 y 时为 0 */
/* 取值为正或负时元素沿着坐标轴的旋转方向：x正逆负顺，y正顺负逆*/
transform: skewX(a);
transform: skewY(a);
```

### 3D转换

#### 透视

```css
perspective: none|length
/*none 默认值，不应用透视
  length 指定观察者距离 z=0 平面的距离，当值为 0 或 负值时，无透视变换*/
/*注意：透视属性要写在 被观察元素的父盒子 样式中*/
/*元素在 Z 轴方向上的变化要配合 透视属性的设置 来体现*/
/*默认情况下，消失点(透视视点？) 位于设置了透视属性的元素中心，可以通过 perspective-origin 来改变*/
```

##### 透视原点

```css
perspective-origin: x <y>;
/*指定了观察者的位置*/
/*默认值为 50% 50% ，即在设置了透视属性的元素中心*/
/*x 取值为 left|center|right|length|percentage
  y 取值为 top|center|bottom|length|percentage
  取值 length|percentage 时，可以取负值，百分比是相对于元素宽度的百分比
  当取值均为关键字时，可以调换 x 和 y 的次序
  可以缺省 y ，缺省时为 50% */
```

#### 平移

```css
transform: translate3d(x, y, z);
transform: translateZ(z);
/*x 和 y 取值为 length或percentage，z 只能取值为 length */
/*元素在 Z 轴方向上的变化要配合 透视属性的设置 来体现*/
```

#### 旋转

```css
transform: rotate3d(x, y, z, a);
/*x y z 取值为 number
  a 取值为 angle*/
/*该旋转使元素能绕固定轴移动而不变形，移动量由角度定义
  旋转轴有三个自由度：x y z，且过 转换原点（transform-origin） 
  一般来说旋转轴向量应该为标准化向量——即三个坐标的平方和为1，当不是标准化向量时，将在内部被标准化，不能标准化的向量（如空向量(0, 0, 0)）将导致旋转不被应用*/
```

```css
transform: rotateX(a);
transform: rotateY(a);
transform: rotateZ(a);
/* a 取值为 angle
   rotateX(a) 等同于 rotate(1, 0, 0, a)
   rotateY(a) 等同于 rotate(0, 1, 0, a)
   rotateZ(a) 等同于 rotate(0, 0, 1, a)
*/
```

注意：以上旋转皆绕一个**过转换原点的旋转轴向量**旋转

#### 缩放

 ```css
transform: scale3d(x, y, z);
/* x y z 取值为 number
   x y z 的取值超过[-1, 1]时在相应坐标轴上放大元素，
   在[-1, 1]内时缩小元素
   为1时不会有变化
   当取负值时执行点反射和大小修改*/
 ```

```css
transform: scaleX(s);
transform: scaleY(s);
transform: scaleZ(s);
/* s 取值为 angle */
/* 分别为在 x y z 方向上的缩放*/
```

### 转换样式

```css
transform-style: flat|preserve-3d;
/*设置该 元素的子元素 是位于 平面 还是 3D空间 中*/
/*注意：设置这么一个空间样式应该在元素的父元素中设置*/
```

### 复合写法

**注意：当转换属性中只写单一变换时，只有写在最后的转换会生效**
例如：

```css
/* 并不能通过以下做法实现先平移后旋转 */
transform: translate(x, y);
transform: rotate(angle);
/* 上述样式只有旋转样式会生效，因为写在最后。需要通过下述写法实现 */
transform: translate(x, y) rotate(<angle>);
```

```css
transform: none|<transform-list>
/* <transform-list>表示多个转换函数<transform-function>，这些转换函数包括2D和3D的转换函数*/
/* 每个转换函数用空格隔开 */
/* 转换函数的顺序会影响最后的结果，一般来说如果要实现的转换包括多种基本操作，应该把平移放在最前面，因为需要注意的是 图形旋转后 整个坐标轴也跟着旋转 了，这时候按照原有坐标系来进行平移的结果可能和预期不一致 */
```

## 动画（CSS3）

动画的使用分为两步：定义动画（使用关键帧规则定义），调用动画（`animation`相关属性）

### 关键帧

要使用关键帧, 先创建一个带名称的 `@keyframes` 规则，以便后续通过 `animation-name` 属性将动画同其关键帧声明匹配

```css
@keyframes <keyframes-name> {
    <keyframe-block-list>
}
/* <keyframes-name> = <custom-ident>|<string> */
/* 
<keyframes-block-list> = <keyframe-block>+  
<keyframe-block> = from|to|<percentage> {
	<declaration-list>
}
 各个<keyframe-block>仅需用花括号分隔
 from 等价于 0%，to 等价于 100%
*/

/*关键帧 @keyframes at-rule 规则通过在动画序列中定义关键帧（或waypoints）的样式来控制CSS动画序列中的中间步骤*/
/*每个 @keyframes 规则包含多个关键帧块，也就是一段样式块语句，每个关键帧块有 一个百分比值作为名称，代表在动画进行中，在哪个阶段触发这个帧块所包含的样式*/
/* 关键帧的百分比 可以不按顺序 给出，执行时按照应该发生的顺序处理*/
/* 如果一个关键帧规则没有指定动画的开始或结束状态，将使用元素的现有样式作为起始或结束状态*/
/* 若关键帧的样式中使用了不能用作动画的属性，这些属性会被忽略掉*/
/* 多个关键帧块使用同一个名称，以最后一个定义的为准*/
/* @keyframes不存在层叠样式（cascade）的情况，动画在一个时刻只会使用一个关键帧块的数据*/
/* 关键帧中的 !important 会被忽略掉*/
/* 若一个关键帧块中没有出现其他关键帧块中的属性，那么这个属性若能使用插值则将使用插值，否则忽略*/
```

*和`transition`相比，关键帧`keyframes`可以控制动画序列的中间步骤*

### 常用动画属性

#### animation-name

```css
animation-name: [none|<keyframes-name>]#;
/*属性指定应用的一系列动画，可以有一个或多个关键帧列表的名称，每个名称代表一个由@keyframes定义的动画序列*/
/*none 表示无关键帧，可以不改变其他标识符的顺序而使动画失效，或者使层叠的动画样式失效*/
/*多个值用英文逗号分隔*/
```

#### animation-duration

```css
animation-duration: <time>#;
/*指定一个动画周期的时长*/
/*默认为 0s*/
/*取值为 number + s/ms，负值无效*/
/*多个值用英文逗号分隔*/
```

#### animation-timing-function

```css
animation-timing-function: <timing-function>#;

/*ease|ease-in|ease-out|ease-in-out|linear|step-end|step-start|cubic-bezier(x1, y1, x2, y2)|step(nub_of_step, direction)*/
/*定义动画在每一动画周期中的执行节奏*/
/*对于关键帧动画来说，定时函数作用于一个关键帧周期而非整个动画周期*/
/*定义于一个关键帧块的定时函数应用到该关键帧，若干该关键帧没有定义缓动函数，则使用定义于整个动画的定时函数*/
/*多个值用英文逗号分隔*/
```

#### animation-delay

```css
animation-delay: <time>#;
/*定义动画何时开始，即动画应用到元素上到动画开始的时间长度*/
/*默认为 0s*/
/*取值为 number + s/ms，负值无效*/
/*多个值用英文逗号分隔*/
```

#### animation-iteration-count

```css
animation-iteration-count: [infinite|<number>]#;
/*定义动画结束前运行的次数*/
/*数字取值可以为小数，不可为负值*/
/*多个值用英文逗号分隔*/
```

#### animation-direction

```css
animation-direction: [normal|reverse|alternate|alternate-reverse]#;
/*指示动画是否反向播放*/
/*normal 默认值，每个动画循环结束则重置到起点重新开始
  reverse 反向运行动画，每周期结束动画由尾到头运行
  alternate 动画交替反向运行，反向运行时，动画按步后退，且带时间功能的函数也反向
  alternate-reverse 动画也是交替反向运行，但是动画第一次运行时原来方向的反向*/
/*多个值用英文逗号分隔*/
```

#### animation-fill-mode

```css
animation-fill-mode: [none|forwards|backwards|both]#;
/*设置动画在执行之前和之后如何将样式应用于目标*/
/*none 默认值，动画未执行时，动画不会将任何样式应用于目标
  forwards 目标将保留 执行期间遇到的 最后一个关键帧 计算值
  backwards 动画将在应用于目标时 立即应用 第一个关键帧 中定义的值，且在animation-delay期间保留此值，但注意：目标并不保留执行期间遇到的任何关键帧计算值
  both 动画将遵循 forwards 和 backwards 的规则，从而在两个方向上扩展动画属性，即动画会立即应用第一个关键帧中的样式，并且目标将保留执行期间遇到的最后一个关键帧计算值*/
/*多个值用英文逗号分隔*/
```

#### animation-play-state

```css
animation-play-state: [running|paused]#;
/*定义一个动画是否运行或暂停*/
/*running 默认值，当前动画正在运行
  paused 当前动画已被停止*/
/*可以配合伪类使用（如:hover）*/
```

#### animation

```css
animation: none|name duration timing-function delay iteration-count direction fill-mode play-state;
/*对于 *-duration 和 *-delay 在简写属性中的解析，当只有一个 <time> 值时会被解析为 *-duration ，当有两个时，写在前面的解析为 *-duration ，后面的解析为 *-delay */
/*简写属性的值不必严格按照上述顺序，但尽量这么写*/
/*对于简写属性中的 *-play-state 值，部分教程说不能写在其中，但经过实践证明可以*/
/*多个动画用英文逗号分隔*/
```

## 浏览器私有前缀

浏览器私有前缀是为了兼容老版本的写法，比较新的浏览器无须添加

### 私有前缀

`-moz-`: 代表 firefox 浏览器私有前缀

`-ms-`: 代表 ie浏览器私有属性

`-webkit-`: 代表 safari、chrome 私有属性

`-o-`: 代表 Opera 私有属性

