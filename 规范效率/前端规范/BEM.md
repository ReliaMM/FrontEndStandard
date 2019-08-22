## BEM介绍

### BEM是什么
- BEM是一套CSS*国际命名规范*，是一个非常有用的功能强大且简单的命名约定，它能使前端代码更*易读易理解易扩展*。

### 为什么要使用BEM方式命名
- BEM的关键特征就是*块的独立性*。按照CSS的建议，可以在网页上的任何位置放置一个块，并确保不会受到周围环境的影响。而且，如果您最近需要将另一个块嵌套到当前块中，则它们的完全兼容性将得到保证。换句话说，在维护Web应用程序时，您可以在*整个页面上移动块*，*添加其他项并将其组合起来*。

- 它传达目的或功能
- 它传达组件结构
- 它为样式选择器设置了一致的低级别特异性

### BEM构成
- BEM类名称最多包含三个部分
  - 块：组件的最外层父元素被定义为块。
  - 元素：组件内部可以是一个或多个称为元素的子元素。
  - 修饰符：块或元素可能具有由修饰符表示的变体
  [block]__[element]--[modifier]

block 代表了更高级别的抽象或组件。 *Block不是BEM血统的开始，它是统一的因素*。此外，元素不是由他们的祖先定义的; 相反，它们是由它们在*Block中的目的*来定义的。
block__element 代表 .block 的后代，用于*形成一个完整的 .block 的整体*。
block--modifier 代表 .block 的不同状态或不同版本。使用两个连字符和下划线而不是一个，是为了让你自己的块可以用单个连字符来界定。如：
.sub-block__element {}
.sub-block--modifier {}

### 例子
#### 不要单独使用修饰符类。修饰符类旨在扩充而不是替换基类。

>组件可能有变化。应使用修饰符类实现变体。
```html
<!-- DO THIS -->
<button class="btn btn--secondary"></button>

<style>
  .btn {
    display: inline-block;
    color: blue;
  }
  .btn--secondary {
    color: green;
  }  
</style>

<!-- DON'T DO THIS -->
<button class="btn--secondary"></button>

<style>
  .btn--secondary {
    display: inline-block;
    color: green;
  }  
</style>  
```

#### 元素组件
>BEM背后的目的之一是保持特异性低且一致。不要忽略HTML中子元素的类名。这将迫使你使用一个选择增加特异性的样式组件内的裸露元素（见img和figcaption下面的元素）。离开这些课程可能会更简洁，但您将来会增加级联问题的风险。BEM的一个目标是*大多数选择器只使用一个类*名。BEM类旨在为单个元素提供唯一的类名
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
>如果您的组件具有多个级别的子元素，请不要尝试表示类名中的每个级别。*BEM无意传达结构深度*。表示组件中子元素的BEM类名称应仅包含基本/块名称和一个元素名称。在下面的示例中，请注意photo__caption__quoteBEM的使用不正确，但photo__quote更合适。
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
>在某些情况下，您可能希望改变组件中的*单个元素*。在这些情况下，为元素而不是组件添加修饰符。我发现修改元素比修改整个组件要少得多，也没那么有用。
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
>如果您发现自己*以相同的方式一致地修改*同一组件的元素，则考虑将修改器添*加到组件的基础*，并基于该修饰符调整每个子元素的样式。这将增加特异性，但它使修改组件更加简单。
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
>BEM名称故意使用双下划线和双连字符而不是单个来分隔块元素修饰符。原因是*单个连字符可以用作单词分隔符*。类名应该是非常易读的，因此除非缩写是普遍可识别的，否则并不总是需要缩写。

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


### 请阅读
- [小鼠和BEM：用CSS组织解决常见问题](https://seesparkbox.com/foundry/bem_css_organization)
- [BEM](http://getbem.com/introduction/)
- [BEM](https://en.bem.info/methodology/css/)
- [BEM](https://seesparkbox.com/foundry/bem_by_example)