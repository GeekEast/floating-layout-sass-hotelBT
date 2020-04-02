<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Table Of Content

- [sass: 预处理器](#sass-%E9%A2%84%E5%A4%84%E7%90%86%E5%99%A8)
  - [Variables](#variables)
    - [声明](#%E5%A3%B0%E6%98%8E)
    - [引用](#%E5%BC%95%E7%94%A8)
  - [Nesting](#nesting)
    - [css](#css)
    - [scss](#scss)
    - [attribute nesting](#attribute-nesting)
  - [Partial](#partial)
    - [声明](#%E5%A3%B0%E6%98%8E-1)
    - [使用](#%E4%BD%BF%E7%94%A8)
    - [架构](#%E6%9E%B6%E6%9E%84)
  - [Function](#function)
  - [Mixin](#mixin)
    - [声明](#%E5%A3%B0%E6%98%8E-2)
    - [使用](#%E4%BD%BF%E7%94%A8-1)
  - [Inheritance](#inheritance)
    - [声明](#%E5%A3%B0%E6%98%8E-3)
    - [引用](#%E5%BC%95%E7%94%A8-1)
  - [Condition Styles](#condition-styles)
    - [@if](#if)
    - [@else](#else)
    - [ternary](#ternary)
  - [Loop: Batch Selectors](#loop-batch-selectors)
    - [for](#for)
    - [each](#each)
    - [while](#while)
- [sass: 为了`复用`而生](#sass-%E4%B8%BA%E4%BA%86%E5%A4%8D%E7%94%A8%E8%80%8C%E7%94%9F)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

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


