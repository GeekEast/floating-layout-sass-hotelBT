## sass: 预处理器
### variables
- 可在**任意位置**声明
- 需用`@import`
- 插值使用`#{$..}`
#### 声明
```scss
$small: 5;
```
#### 引用
```scss
@import "variables";
div {
  font-size: #{$small}px
}
```

### Nesting
- `&`代表**当前层**元素
- **css属性**也可以nesting, 但是存在bug
#### css
```scss
ul li {}
```
#### scss
```scss
ul {
  li {}
}
```
