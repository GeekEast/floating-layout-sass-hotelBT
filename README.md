## sass: 预处理器
- 使用了**一**次`@import`之后, `variables`, `functions`, `mixins`, `inheritance`都是全局可见的，无需在单个文件中再次`@import`

### Variables
- 可在**任意位置**声明
- 需用`@import`
- **插值**使用`#{$..}`

#### 声明
```scss
$small: 5;
```

#### 引用
```scss
div {
  font-size: #{$small}px
}
```

### Nesting
- `&`代表**当前层**元素
#### css
```scss
ul li {}
```
#### scss
```scss
ul {
  li {//}
}
```
#### attribute nesting
- `border`后面必须加**冒号**
```scss
　　p {
　　　　border: {
　　　　　　color: red;
　　　　}
　　}
```

### Partial
- a piece of scss code
- **won't generate css file**, will be **integrated** into another scss/sass file.
  
#### 声明
`_color.scss`

#### 使用
```scss
@import 'color'
```

#### 架构
- 全局只有**一**个非partial文件, 无法按需引入
- 全局有很**多**个非partial文件，可以按需引入

### Function
- 产生值的函数
```scss
@function func_name() {
  // function body
  @return res;
}
```

### Mixin
- 产生`属性集合`的一种**特殊函数**
- 跟`继承`相比，最强大的地方是可以提供`参数`
#### 声明
```scss
@mixin name {
  // css properties;
}

@mixin name(parameter) {
  // css properties;
}
```
#### 使用
```scss
.test {
  @include name;
}
```

### Inheritance
- `@extend`嵌套会增加**权重**
#### 声明
- 类: `.box {...}`
- 抽象类: `%box {...}`
- `类`已经生效,而`抽象类`作为`模板`，只有在被`@extend`之后才起效果
#### 引用
- 类: `@extend .box`
- 抽象类: `@extend %box`

### Condition Styles
#### @if
```scss
p {
　　@if (1 + 1 == 2) { border: 1px solid; }
　　@if (5 < 3) { border: 2px dotted; }
}
```
#### @else
```scss
@if () {

} @else {

}
```
#### ternary
```scss
@if (condition, default, otherwise)
```
### Loop: Batch Selectors
#### for
```scss
@for $i from 1 through 20 {

}
```
#### each
```scss
@each $i in $colors {

}
```
#### while
```scss
$i: 6;

@while $i > 0 {
　　.item-#{$i} { width: 2em * $i; }
　　$i: $i - 2;
}
```

## sass: 为了`复用`而生


