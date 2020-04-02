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
  - [复用分级](#%E5%A4%8D%E7%94%A8%E5%88%86%E7%BA%A7)
    - [变量层面](#%E5%8F%98%E9%87%8F%E5%B1%82%E9%9D%A2)
    - [函数层面](#%E5%87%BD%E6%95%B0%E5%B1%82%E9%9D%A2)
    - [对象层面](#%E5%AF%B9%E8%B1%A1%E5%B1%82%E9%9D%A2)
  - [单位重设](#%E5%8D%95%E4%BD%8D%E9%87%8D%E8%AE%BE)
  - [工具类情景](#%E5%B7%A5%E5%85%B7%E7%B1%BB%E6%83%85%E6%99%AF)
    - [快速布局](#%E5%BF%AB%E9%80%9F%E5%B8%83%E5%B1%80)
    - [临时状态](#%E4%B8%B4%E6%97%B6%E7%8A%B6%E6%80%81)
  - [选择器情景](#%E9%80%89%E6%8B%A9%E5%99%A8%E6%83%85%E6%99%AF)
    - [批量属性](#%E6%89%B9%E9%87%8F%E5%B1%9E%E6%80%A7)
    - [内部细节](#%E5%86%85%E9%83%A8%E7%BB%86%E8%8A%82)

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
- 全局有很**多**个非partial文件, 可以按需引入

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
### 复用分级
#### 变量层面
- `numeric`
- `string`
- `list`
- `map`
- ...
#### 函数层面
- `function`
- `mixin`
#### 对象层面
- 实体类 `.`
  - 工具类 `.current .text-orange`
  - 组件类 `.btn`
- 抽象类 `%`
### 单位重设
- `数字`: **5**
- `百分比`: **5%**
- `Divide`: **1**
### 工具类情景
- `松散分布`时使用
#### 快速布局 
```html
<div class="fl-3 pt-3"><.div>
```
#### 临时状态 
```html
<div class="current"></div>
```
### 选择器情景
- `集中分布`时使用
#### 批量属性
- html
```html
<ul>
  <li></li>
  <li></li>
  <li></li>
</ul>
```
- css
```css
ul li {
  /* style */
}
```
#### 内部细节
- html
```html
<nav id="navbar">
  <div class="container">
    <h1 class="logo">
      <a href="index.html">HBT</a>
    </h1>
    <ul>
      <li class="current"><a href="index.html">Home</a></li>
      <li ><a href="about.html">About</a></li>
      <li ><a href="contact.html">Contact</a></li>
    </ul>
  </div>
</nav>
```
- css
```css
#navbar {
  @extend .bg-black;
  .logo {
    @extend .fl;
    @extend .p-2;
    @extend .hr_a-text-orange;
  }
  ul {
    @extend .fp;
    @extend .fr;

    li {
      @extend .fl;
      @extend .p-3;
      @extend .hr_a-text-orange;
      @extend .hr-bg-grey;
    }
  }
}
```
