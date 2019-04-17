# Airbnb CSS / Sass 风格规范

*可能是最合理使用CSS和Sass的方法*

## 索引

1. [术语--Terminology](#术语--terminology)
    - [规则声明--Rule Declaration](#规则声明--rule-declaration)
    - [选择器--Selectors](#选择器--selectors)
    - [属性--Properties](#属性--properties)
1. [CSS](#css)
    - [格式化--Formatting](#格式化--formatting)
    - [注释--Comments](#注释--comments)
    - [面向对象CSS和BEM--OOCSS and BEM](#面向对象css和bem--oocss-and-bem)
    - [ID选择器--ID Selectors](#id选择器--id-selectors)
    - [JavaScript钩子--JavaScript hooks](#JavaScript钩子--javascript-hooks)
    - [变框--Border](#边框--border)
1. [Sass](#sass)
    - [语法--Syntax](#语法--syntax)
    - [属性声明排序](#属性声明排序--ordering-of-property-declarations)
    - [变量--Variables](#变量--variables)
    - [混合--Mixins](#混合--mixins)
    - [扩展指令--Extend directive](#扩展指令--extend-directive)
    - [嵌套选择器--Nested selectors](#嵌套选择器--nested-selectors)
1. [翻译--Translation](#翻译--translation)
1. [License](#license)

## 术语--Terminology

### 规则声明--Rule declaration

规则声明（ “rule declaration”） 就是给一个或一组选择器名字同时伴随一组属性。看下面的例子:

```css
.listing {
  font-size: 18px;
  line-height: 1.2;
}
```

### 选择器--Selectors

在规则声明中，选择器决定了DOM树中那些元素将被定义的属性设置样式。选择器可以匹配HTML元素，也可以是元素的类(class),ID,或者其它任何属性。下面是一些选择器相关的例子：

```css
.my-element-class {
  /* ... */
}

[aria-hidden] {
  /* ... */
}
```

### 属性--Properties

最后，属性给选中的元素规则声明来声明它们的样式。属性时键值对,一个规则声明可以包含一个或多个属性声明。属性声明如下：

```css
/* some selector */ {
  background: #f1f1f1;
  color: #333;
}
```

**[⬆ 顶部](#索引)**

## CSS

### 格式化--Formatting

* 使用软tabs(2个空格)作为缩进。
* 使用破折号方式命名类而不是驼峰命名(camelCasing)。
  - 下划线和帕斯卡（PascalCasing）也是可以的，如果你使用BEM(参考 [面向对象CSS和BEM](#面向对象css和bem--oocss-and-bem)).
* 不用ID选择器。
* 规则声明中有多个选择器时，每个选择器独占一行。
* 规则声明左括号和选择器直接放置一个空格。
* 属性在`:`字符的后面放一个空格。
* 规则声明的右括号`}`需要当度一行。
* 两个规则声明直接使用空行隔开。

**Bad**

```css
.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
```

**Good**

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```

### 注释--Comments

* 行注释由于块注释(Sass文件中使用`//`)。
* 注释最好在自己的行里，避免跟在属性的后面。
* 不能自描述的代码，要写详细的注释：
  - z-index的作用
  - 兼容性或者浏览器特定的hacks。

### 面向对象和BEM--OOCSS and BEM

我们鼓励OOCSS和BEM这个组合的原因是：

  * 它帮助我们在CSS和HTML直接创建清晰且严格的关系
  * 它帮助我们创建可复用，可组合的组件
  * 它允许更少的嵌套和低特意性
  * 它有助于创建可扩展的样式

**面向对象CSS(OOCSS)**, 或者叫 “Object Oriented CSS”, 是一种编辑CSS的方式，它鼓励你把样式当作一系列的对象：它们可以复用，可以重复的片段，可以独立于网站使用。

  * Nicole Sullivan's [OOCSS wiki](https://github.com/stubbornella/oocss/wiki)
  * Smashing Magazine's [Introduction to OOCSS](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/)

**BEM**, 或者说 “Block-Element-Modifier”, 是HTML和CSS中的类的一种 _命名风格（naming convention）_ 。它最是Yandex开发的考虑到大型代码库和扩展性， 并且可以作为实现OOCSS的一套可靠的指导方针。

  * CSS Trick's [BEM 101](https://css-tricks.com/bem-101/)
  * Harry Roberts' [introduction to BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

我们推荐BEM的一个使用帕斯卡(pascalCased)块的变体,它与组件结合是特别好（比如,React,Vue)。双连字符和破折号仍然用于修饰器（modifiers)和子元素.

**例子**

```jsx
// ListingCard.jsx
function ListingCard() {
  return (
    <article class="ListingCard ListingCard--featured">

      <h1 class="ListingCard__title">Adorable 2BR in the sunny Mission</h1>

      <div class="ListingCard__content">
        <p>Vestibulum id ligula porta felis euismod semper.</p>
      </div>

    </article>
  );
}
```

```css
/* ListingCard.css */
.ListingCard { }
.ListingCard--featured { }
.ListingCard__title { }
.ListingCard__content { }
```

  * `.ListingCard` 是块(“block”)表示更高层级的组件
  * `.ListingCard__title` 是元素（“element”)表示`.ListingCard`的后代，该子代有助于将块组成一个整体
  * `.ListingCard--featured` 是一个修饰符表示`.ListingCard`块的不同的状态或者变化。

### ID选择器--ID selectors

虽然可以在CSS中按ID选择元素,但通常应将其视为反模式(anti-pattern)。ID选择器引入了一个不需要的高级[特性](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)到规则声明中，并且它们不可复用。

有关此主题的更多信息， 阅读 [CSS Wizardry's 文章](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) 关于特性的处理.

### JavaScript钩子--JavaScript hooks

在CSS和JavaScript中，避免绑定到同一个类。将这两者结合起来轻则导致在重构过程中浪费时间，同时开发人员必须交叉引用他们正在更改的每个类，更糟糕的是开发人员害怕进行更改，以免破坏功能。

我们推荐创建JavaScript特有的类来绑定,前缀为`.js-`：

```html
<button class="btn btn-primary js-request-to-book">Request to Book</button>
```

### 边框-Border

使用 `0` 代替`none`来指定一个样式没有边框。

**Bad**

```css
.foo {
  border: none;
}
```

**Good**

```css
.foo {
  border: 0;
}
```

**[⬆ 顶部](#索引)**

## Sass

### 语法--Syntax

* 使用`.scss`语法,不用原先的`.sass`语法
* 对常规的CSS和`@include`声明进行逻辑排序(详情如下)

### 属性声明排序--Ordering of property declarations

1. 属性声明

    列出所有标准属性声明，任何不是`@include或嵌套选择器的声明。

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      // ...
    }
    ```

2. `@include` 声明

    最后对`@include`进行分组，这样更容易地读取整个选择器。

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);
      // ...
    }
    ```

3. 嵌套选择器--Nested selectors

    嵌套选择器,_如果必需_,到最后并且没有任何内容在它后面。在规则声明和嵌套选择器之间添加空行,以及相邻选择器之间也是如此。对嵌套选择器运用和上面相同的指导原则。

    ```scss
    .btn {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);

      .icon {
        margin-right: 10px;
      }
    }
    ```

### 变量--Variables

与驼峰命名（camelCased)和蛇形命名（sname_cased）相比，首先破折号命名(dash-cased)变量(例如$my-variable)。可以接受的做法是在变量名前加下划线（比如`$_my-variable`),这些变量只能在同一个文件中使用。

### 混合--Mixins

混合被用来DRY(Don't repeat youself)你的代码，增加清晰性和抽象复杂性--这与命名函数的方式基本一样。不接受任何参数的mixin可能对此很有用，但请注意，如果不压缩有效负载（例如gzip），这可能会导致生成的样式中出现不必要的代码重复。

### 扩展指令--Extend directive

扩展(`@extend`)应该避免因为它有非故意的和潜在的微信行为,特别当和嵌套选择器一起使用。即使扩展顶级站位符选择器如果选择器的位置稍后发生改变也可能导致问题（比如它们咋其他文件中，并且文件的加载属性发生了改变）。Gzipping应该能够处理大部分通过使用`@extend`获得的节省,并且你你可以和好的用混合（mixins） DRY你的样式。

### 嵌套选择器--Nested selectors

**不要嵌套选择器超过三层深度！**

```scss
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```

当选择器变长时，你可能在按下面的方式写CSS：

* 与HTML强耦合(脆弱的) *—OR—*
* 过于具体 (有力的) *—OR—*
* 没有复用

再次: **从不嵌套ID选择器**

若果你必须首先使用ID选择器(并且你确实应该尝试不使用)，则不应该嵌套他们。如果你发现自己做了这些,那么你需啊重新访问标记，或者指出为什么需要这么强的特异性。如果你正在编写格式良好的HTMl和CSS,你应该**永远不需要**这样做。

**[⬆ 顶部](#索引)**

## 翻译--Translation

  这份风格指南还提供其它的语言版本：

  - ![id](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Indonesia.png) **Bahasa Indonesia**: [mazipan/css-style-guide](https://github.com/mazipan/css-style-guide)
  - ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Chinese (Traditional)**: [ArvinH/css-style-guide](https://github.com/ArvinH/css-style-guide)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [Zhangjd/css-style-guide](https://github.com/Zhangjd/css-style-guide)
  - ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **French**: [mat-u/css-style-guide](https://github.com/mat-u/css-style-guide)
  - ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [nao215/css-style-guide](https://github.com/nao215/css-style-guide)
  - ![ko](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [CodeMakeBros/css-style-guide](https://github.com/CodeMakeBros/css-style-guide)
  - ![PT-BR](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Portuguese (Brazil)**: [felipevolpatto/css-style-guide](https://github.com/felipevolpatto/css-style-guide)
  - ![pt-PT](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Portugal.png) **Portuguese (Portugal)**: [SandroMiguel/airbnb-css-style-guide](https://github.com/SandroMiguel/airbnb-css-style-guide)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**: [rtplv/airbnb-css-ru](https://github.com/rtplv/airbnb-css-ru)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [ismamz/guia-de-estilo-css](https://github.com/ismamz/guia-de-estilo-css)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnamese**: [trungk18/css-style-guide](https://github.com/trungk18/css-style-guide)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**: [antoniofull/linee-guida-css](https://github.com/antoniofull/linee-guida-css)
  - ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **German**: [tderflinger/css-styleguide](https://github.com/tderflinger/css-styleguide)

**[⬆ 顶部](#索引)**

## License

(The MIT License)

Copyright (c) 2015 Airbnb

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ 顶部](#索引)**