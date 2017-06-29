#### Flex布局

> flex属性用于设置或者检索弹性盒子模型对象的子元素如何分配空间。
>
> flex属性是：`felx-grow,flex-shrink,flex-basis`属性的简写。
>
> 注意：*如果元素不是弹性盒子模型对象的子元素，则flex属性将不起作用*
>
> ```css
> flex: flex-grow flex-shrink flex-basis|auto|initial|inherit
> ```
>
> |      值      |                    描述                    |
> | :---------: | :--------------------------------------: |
> |  flex-grow  |        一个数字，规定项目将相对于其他灵活项目进行扩展的量         |
> | flex-shrink |         一个数字，规定项目相对于其他灵活项目进行收缩的量         |
> | flex-basis  | 规定灵活项目的初始长度。合法值：auto,inherit，或者N(%,px,em,...) |
> |    auto     |                等同1 1 auto                |
> |    none     |                 0 0 auto                 |
> |   initial   |               默认值：0 1 auto               |
> |   inherit   |                  继承父元素                   |
>
> ##### flex-direction 
>
> > 规定灵活项目的方向
> >
> > ```css
> > flex-direction:row | row-reverse | column | column-reverse |initial | inherit
> > ```
> >
> > |       值        | 描述            |
> > | :------------: | ------------- |
> > |      row       | 默认值。灵活项目水平显示  |
> > |  row-reverse   | 水平显示，但是以相反方向  |
> > |     column     | 灵活项目将垂直显示     |
> > | column-reverse | 垂直显示，但是以相反的顺序 |
> > |    initial     | 设置为默认值        |
> > |    inherit     | 继承父元素         |
>
> ##### flex-wrap
>
> > 规定灵活元素是否拆行或者拆列
> >
> > ```css
> > flex-wrap: nowrap | wrap | wrap-reverse | initial |inherit
> > ```
> >
> > |      值       |       描述        |
> > | :----------: | :-------------: |
> > |    nowrap    |  默认值。不拆行或者不拆列   |
> > |     wrap     |     拆行或者拆列      |
> > | wrap-reverse | 拆行或者拆列，但是以相反的顺序 |
> > |   initial    |   设置该属性为其默认值    |
> > |   inherit    |      继承父元素      |
>
> ##### flex-flow
>
> > flex-flow属性是flex-direction和flex-wrap属性的复合属性
> >
> > flex-flow属性用于设置或者检索弹性盒子模型对象的子元素的排列顺序
> >
> > flex-direction规定灵活项目的方向，flex-wrap规定 灵活项目是否拆行或者拆列
> >
> > ```css
> > flex-flow: flex-direction flex-wrap | initial |inherit;
> > ```
>
> ##### flex-grow
>
> > 规定弹性盒子模型的扩展比率
> >
> > ```css
> > flex-grow: number | initial |inherit
> > ```
> >
> > 规定项目对于其他灵活项目进行扩展的量
>
> ##### flex-shrink
>
> > 规定弹性盒子模型的收缩比率
> >
> > ```css
> > flex-shrink: number | initial |inherit
> > ```
> >
> > 规定灵活项目相对于其他灵活项目进行收缩的量，默认0.
>
> ##### justify-content
>
> > 规定项目在主轴上的对齐方式
> >
> > ```css
> > justify-content: flex-start | flex-end | center | space-betwwen | space-around
> > ```
> >
> > |       值       |      描述       |
> > | :-----------: | :-----------: |
> > |  flex-start   |   左对齐（默认值）    |
> > |   flex-end    |      右对齐      |
> > |    center     |      居中       |
> > | space-between | 两端对齐，项目间的间隔相等 |
> > | space-around  | 每个项目的两侧的间隔相等  |
>
> ##### align-items
>
> > 规定项目在交叉轴上如何对齐
> >
> > ```css
> > align-items: flex-start | flex-end | center  | baseline | stretch
> > ```
> >
> > |     值      |                描述                 |
> > | :--------: | :-------------------------------: |
> > | flex-start |               起点对齐                |
> > |  flex-end  |               终点对齐                |
> > |   center   |               中点对齐                |
> > |  baseline  |           项目第一行文字的基线对齐            |
> > |  stretch   | 默认值。如果项目未舍子高度或者舍子为auto，将占满真个容器的高度 |
>
> ##### align-content
>
> 规定多根轴线的对齐方式
>
> ```css
> align-content: flex-start | flex-end | center | stretch |spance-between | space-around 
> ```
>
> - `flex-start`：与交叉轴的起点对齐。
> - `flex-end`：与交叉轴的终点对齐。
> - `center`：与交叉轴的中点对齐。
> - `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
> - `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
> - `stretch`（默认值）：轴线占满整个交叉轴。
>
> ##### order
>
> > 规定项目的排列顺序，数值越小排列越靠前，默认为0
> >
> > ```css
> > order: number
> > ```
>
> ##### align-self
>
> > 允许单个项目与其他项目不一样的对齐方式，覆盖align-items 属性，默认auto,表示继承父元素的align-items属性，若没有父元素，则相当stretch
> >
> > ```css
> > align-self: auto | flex-start | flex-end | center | baseline | stretch;
> > ```
> >
> > 