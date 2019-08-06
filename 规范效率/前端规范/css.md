## [BEM](https://seesparkbox.com/foundry/bem_by_example)

### 目录
- 整体规范
  - 前提
  - 不要单独使用修饰符类。修饰符类旨在扩充而不是替换基类。
  - 元素组件
  - 元素与修饰符
  - 基于组件修饰符的样式元素
  - 多字名称
- 多次出现的颜色值抽离
- 公共样式抽离
- 避免deep使用
- 避免直接找到元素覆盖样式，创造custome class
- 尽量使用缩写属性
- 0后面不带单位

### 前提
- BEM类名称最多包含三个部分
  - 块：组件的最外层父元素被定义为块。
  - 元素：组件内部可以是一个或多个称为元素的子元素。
  - 修饰符：块或元素可能具有由修饰符表示的变体
  [block]__[element]--[modifier]


### 不要单独使用修饰符类。修饰符类旨在扩充而不是替换基类。
```html
<!-- DON'T DO THIS -->
<button class="btn--secondary"></button>

<style>
  .btn--secondary {
    display: inline-block;
    color: green;
  }  
</style>  
```
### 元素组件
>BEM背后的目的之一是保持特异性低且一致。不要忽略HTML中子元素的类名。这将迫使你使用一个选择增加特异性的样式组件内的裸露元素（见img和figcaption下面的元素）。离开这些课程可能会更简洁，但您将来会增加级联问题的风险。BEM的一个目标是大多数选择器只使用一个类名。BEM类旨在为单个元素提供唯一的类名
```html
<!-- DO THIS -->
<figure class="photo">
  <img class="photo__img" src="me.jpg">
  <figcaption class="photo__caption">Look at me!</figcaption>
</figure>

<style>
  .photo { } /* Specificity of 10 */
  .photo__img { } /* Specificity of 10 */
  .photo__caption { } /* Specificity of 10 */
</style>

<!-- DON'T DO THIS -->
<figure class="photo">
  <img src="me.jpg">
  <figcaption>Look at me!</figcaption>
</figure>

<style>
  .photo { } /* Specificity of 10 */
  .photo img { } /* Specificity of 11 */
  .photo figcaption { } /* Specificity of 11 */
</style>
```
>如果您的组件具有多个级别的子元素，请不要尝试表示类名中的每个级别。BEM无意传达结构深度。表示组件中子元素的BEM类名称应仅包含基本/块名称和一个元素名称。在下面的示例中，请注意photo__caption__quoteBEM的使用不正确，但photo__quote更合适。
```html
<!-- DO THIS -->
<figure class="photo">
  <img class="photo__img" src="me.jpg">
  <figcaption class="photo__caption">
    <blockquote class="photo__quote">
      Look at me!
    </blockquote>
  </figcaption>
</figure>

<style>
  .photo { }
  .photo__img { }
  .photo__caption { }
  .photo__quote { }
</style>


<!-- DON'T DO THIS -->
<figure class="photo">
  <img class="photo__img" src="me.jpg">
  <figcaption class="photo__caption">
    <blockquote class="photo__caption__quote"> <!-- never include more than one child element in a class name -->
      Look at me!
    </blockquote>
  </figcaption>
</figure>

<style>
  .photo { }
  .photo__img { }
  .photo__caption { }
  .photo__caption__quote { }
</style>


```
### 元素与修饰符
>在某些情况下，您可能希望改变组件中的单个元素。在这些情况下，为元素而不是组件添加修饰符。我发现修改元素比修改整个组件要少得多，也没那么有用。
```html
<figure class="photo">
  <img class="photo__img photo__img--framed" src="me.jpg">
  <figcaption class="photo__caption photo__caption--large">Look at me!</figcaption>
</figure>

<style>
  .photo__img--framed {
    /* incremental style changes */
  }
  .photo__caption--large {
    /* incremental style changes */
  }
</style>
```
### 基于组件修饰符的样式元素
>如果您发现自己以相同的方式一致地修改同一组件的元素，则考虑将修改器添加到组件的基础，并基于该修饰符调整每个子元素的样式。这将增加特异性，但它使修改组件更加简单。
```html
<!-- DO THIS -->
<figure class="photo photo--highlighted">
  <img class="photo__img" src="me.jpg">
  <figcaption class="photo__caption">Look at me!</figcaption>
</figure>

<style>
  .photo--highlighted .photo__img { }
  .photo--highlighted .photo__caption { }
</style>

<!-- DON'T DO THIS -->
<figure class="photo">
  <img class="photo__img photo__img--highlighted" src="me.jpg">
  <figcaption class="photo__caption photo__caption--highlighted">Look at me!</figcaption>
</figure>

<style>
  .photo__img--highlighted { }
  .photo__caption--highlighted { }
</style>
```
### 多字名称
>BEM名称故意使用双下划线和双连字符而不是单个来分隔块元素修饰符。原因是单个连字符可以用作单词分隔符。类名应该是非常易读的，因此除非缩写是普遍可识别的，否则并不总是需要缩写。

```html
<!-- DO THIS -->
<div class="some-thesis some-thesis--fast-read">
  <div class="some-thesis__some-element"></div>
</div>

<style>
  .some-thesis { }
  .some-thesis--fast-read { }
  .some-thesis__some-element { }
</style>

<!-- DON'T DO THIS -->
// These class names are harder to read
<div class="somethesis somethesis--fastread">
  <div class="somethesis__someelement"></div>
</div>

<style>
  .somethesis { }
  .somethesis--fastread { }
  .somethesis__someelement { }
</style>
```


[小鼠和BEM：用CSS组织解决常见问题](https://seesparkbox.com/foundry/bem_css_organization)
[BEM](http://getbem.com/introduction/)
[BEM](https://en.bem.info/methodology/css/)