# Google HTML/CSS 样式指南

> [原文链接](https://google.github.io/styleguide/htmlcssguide.html)

## 目录

  1. [背景](#背景)
  1. [通用规则](#通用规则)
  1. [通用风格规则](#通用风格规则)
  1. [通用格式化规则](#通用格式化规则)
  1. [通用元规则](#通用元规则)
  1. [HTML规则](#html规则)
  1. [HTML风格规则](#html风格规则)
  1. [HTML格式化规则](#html格式化规则)
  1. [HTML元规则](#html元规则)
  1. [CSS规则](#css规则)
  1. [CSS风格规则](#css风格规则)
  1. [CSS格式化规则](#css格式化规则)
  1. [CSS元规则](#css元规则)
  1. [题外话](#题外话)

## 背景
  
  <a name="background" /><a name="1.1"></a>
  - [1.1](#background)本文档定义了HTML和CSS的格式和样式规则。它旨在改善协作，代码质量和支持基础架构。他适用于使用HTML和CSS的原始工作文件。只要保持通用代码质量，工具就可以自由地进行模糊处理，缩小和编译。

## 通用规则

### 通用风格规则

  <a name="protocol" /><a name="2.1"></a>
  - [2.1](#protocol) 对于嵌入资源尽可能的使用HTTPS协议。总是使用 HTTPS 协议(`https:`)加载图片和其他媒体文件，样式表还有脚本除非是不支持HTTPS的。

  ```html
  <!-- 不推荐: 省略了协议 -->
  <script src="//ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>

  <!-- 不推荐: 使用 HTTP 协议 -->
  <script src="http://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>

  <!-- 推荐 -->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
  ```

  ```css
  /* 不推荐: 省略了协议 */
  @import '//fonts.googleapis.com/css?family=Open+Sans';

  /* 不推荐: 使用 HTTP 协议 */
  @import 'http://fonts.googleapis.com/css?family=Open+Sans';

  /* 推荐 */
  @import 'https://fonts.googleapis.com/css?family=Open+Sans';
  ```

**[⬆ 顶部](#目录)**

### 通用格式化规则

  <a name="indentation" /><a name="2.2"></a>
  - [2.2](#indentation) 每次使用2个空格缩进。 不要使用tabs或者混用tabs和空格来缩进。

  ```html
  <ul>
      <li>Fantastic
      <li>Great
  </ul>
  ```

  ```css
  .example {
      color: blue;
  }
  ```

  <a name="capitalization" /><a name="2.3"></a>
  - [2.3](#capitalization) 只使用小写。

  > 所有代码用小写。包括：HTML元素名，属性名，属性值（除非`text/CDATA`），CSS选择器，属性和属性值（字符串例外）

  ```html
  <!-- 不推荐 -->
  <A HREF="/">Home</A>
  <!-- 推荐 -->
  <img src="google.png" alt="Google">
  ```

  ```css
  /* 推荐 */
  color: #E5E5E5;
  /* 推荐 */
  color: #e5e5e5;
  ```

  <a name="trailing-whitespace" /><a name="2.4"></a>
  - [2.4](#trailing-whitespace) 删除尾随空格。

  > 尾随空格是非必需的同时使得复杂化diffs

  ```html
  <!-- 不推荐 -->
  <p>What?_
  <!-- 推荐 -->
  <p>Yes please.
  ```

**[⬆ 顶部](#目录)**

### 通用元规则

  <a name="encoding" /><a name="3.1"></a>
  - [3.1](#encoding) 使用UTF-8编码（非 BOM)

  > 确保你的编译器UTF-8当做字符编码,没有字节序标志(BOM)。
  > 通过`<meta charset="utf-8">` 在HTML模板和文档中指定编码。不要指定样式表的编码，因他们假定为UTF-8。
  > (更多编码何时和如何指定可以参考[Handing character encodings in HTML and CSS](https://www.w3.org/International/tutorials/tutorial-char-enc/))

  <a name="comments" /><a name="3.2"></a>
  - [3.2](#comments) 在可能的情况下，根据需要注释代码。

  > 用注释解释代码： 它包括什么，它有什么用途, 为什么它是首选或使用的方案。
  > （此项是可选的，因为总是全文档化的代码不被认为是符合实际的。根据项目的复杂程度，HTML和CSS的文档要求是波动很大的）

  <a name="action-items" /><a name="3.3"></a>
  - [3.3](#action-items) 使用`TODO`标记将要做的和具体的操作项

  > 通过使用关键字`TODO`高亮将要去做的事。
  > 联系信息（用户名或者邮件)添加在括号中时用此格式：`TODO(contact)`。
  > 操作项添加在分号后面，比如：`TODO: action item`。

  ```html
  {# TODO(john.doe): 再次讨论居中 #}
  <center>Test</center>

  <!-- TODO: 上传选项标记 -->
  <ul>
      <li>Apples</li>
      <li>Oranges</li>
  </ul>
  ```

**[⬆ 顶部](#目录)**

## HTML规则

### HTML风格规则

  <a name="document-type" /><a name="4.1"></a>
  - [4.1](#document-type) 使用HTML5。

  > HTML5（HTML 语法）是所有HTML文档的首选：`<!DOCTYPE html>`
  > (推荐使用HTML文本为`text/html`类型。不要使用XHTML。XHTML是`application/xhtml+xml`类型,在浏览器和基础设施两个方面都缺少支持同时比HTML更少优化的空间。)
  > 虽然HTML很好，但是不要闭合非闭合的元素比如：用`<br>`,不用`<br />`。

  <a name="html-validity" /><a name="4.2"></a>
  - [4.2](#html-validity) 在可能的情况下，使用合法的HTML

  > 使用合法的HTML代码，除非由于无法达到的文件大小性能目标而无法实现。
  > 使用[W3C HTML 验证器](https://validator.w3.org/nu/)进行校验。
  > 使用有效的HTML是一个可衡量的基线质量属性，有助于学习技术要求和约束，从而确保正确的HTML使用。

  ```html
  <!-- 不推荐 -->
  <title>Test</title>
  <article>This is only a test.
  ```

  ```html
  <!-- 推荐 -->
  <!DOCTYPE html>
  <html>
      <head>
          <meta charset="utf-8">
          <title>Test</title>
      </head>
      <body>
          <article>This is only a test.</article>
      </body>
  </html>
  ```

  <a name="semantics" /><a name="4.3"></a>
  - [4.3](#semantics) 语义化：根据其用途使用HTML。

  > 使用元素`elements`（有时被错误的称作标记`tags`)按照其被创建的目的来使用。例如：使用标题元素(`h`)作为标题,段落元素(`p`)代表段落，`a`元素表示锚，等等。
  > 根据其用途使用HTML对于提升可访问性，重用和代码效率来说很重要。

  ```html
  <!-- 不推荐 -->
  <div onclick="goToRecommendations();">All recommendations</div>

  <!-- 推荐 -->
  <a href="recommendations/">All recommendations</a>
  ```

  <a name="multimedia-fallback" /><a name="4.4"></a>
  - [4.4](#multimedia-fallback) 多媒体后备： 给多媒体提供备案。

  > 对于多媒体，像图片，视频，canvas 动画对象，确保提供备用选项。就图片而言这意味使用有意义的备选文案(`alt`)至于如果可能的话视频(`video`)和音频(`audio`)使用副本和字幕。
  > 提供备案对可访问性很重要,原因是：没有`@alt`无法提示盲人用户图片是内容是关于什么的, 其他用户没有办法了解视频和音频的内容。
  > (对于图片它的`alt`属性引入了冗余度，对于那些单纯用来装饰同时无法立即使的css生效的图片,不需要备选文案，比如`alt=""`)

  ```html
  <!-- 不推荐 -->
  <img src="spreadsheet.png">
  <!-- 推荐 -->
  <img src="spreadsheet.png" alt="Spreadsheet screenshot.">
  ```

  <a name="separation-of-concerns" /><a name="4.5"></a>
  - [4.5](#separation-of-concerns) 关注点分离： 结构与行为和表现分离。

  > 严格保证结构（markup），表现（styling)，还有行为（scripting)分离，同时尝试将三者的交互降到最少。
  > 更确切的说，确保文档（documents）和模板（templates）仅包含HTML同时HTML只服务于结构。将所有表现移到样式表中，所有行为移到脚本中。
  > 另外，尽可能通过链接的方式引入样式和脚本来保证与文档或模板的关联区域尽肯能小。
  > 结构与表现和行为的分离，对于维护是很重要的。修改HTML的代价总是比更新样式和脚本更大

  ```html
  <!-- 不推荐 -->
  <!DOCTYPE html>
      <title>HTML sucks</title>
      <link rel="stylesheet" href="base.css" media="screen">
      <link rel="stylesheet" href="grid.css" media="screen">
      <link rel="stylesheet" href="print.css" media="print">
      <h1 style="font-size: 1em;">HTML sucks</h1>
      <p>I’ve read about this on a few sites but now I’m sure:
          <u>HTML is stupid!!1</u>
      <center>I can’t believe there’s no way to control the styling of
      my website without doing everything all over again!</center>
    ```

  ```html
  <!-- 推荐 -->
  <!DOCTYPE html>
      <title>My first CSS-only redesign</title>
      <link rel="stylesheet" href="default.css">
      <h1>My first CSS-only redesign</h1>
      <p>I’ve read about this on a few sites but today I’m actually
        doing it: separating concerns and avoiding anything in the HTML of
        my website that is presentational.
      <p>It’s awesome!
  ```

  <a name="entity-references" /><a name="4.6"></a>
  - [4.6](#entity-references) 实体引用: 不要使用实体引用。

  > 有些实体引用是不需要的像`&mdash;`,`&rdquo`或者`&#x263a`,如果小组中的所有编辑者使用的是相同的编码（UTF-8)。唯一的例外是对那些在HTML中有特殊意义的字符（`<`和`&`）以及控制字符还有不肯见字符（像不换行的空格）。

  ```html
  <!-- 不推荐 -->
  The currency symbol for the Euro is &ldquo;&eur;&rdquo;.

  <!-- 推荐 -->
  The currency symbol for the Euro is “€”.
  ```

  <a name="optional-tags" /><a name="4.7"></a>
  - [4.7](#optional-tags) 可选标签: 省略可选的标签。(这条个人不是很赞同,有点激进)

  > 为了文件大小优化以及可扫描性的目的，考虑省略可选标记.[HTML5 指南](https://html.spec.whatwg.org/multipage/syntax.html#syntax-tag-omission)中定义了那些标记可以省略。
  > (这种方法可能需要一个宽限期作为一个更广泛的指导方针，因为它与Web开发人员通常被教授的内容有很大的不同。出于一致性和简单性的原因，最好省略所有可选标记，而不仅仅是一个选择。)

  ```html
  <!--不推荐 -->
  <!DOCTYPE html>
  <html>
      <head>
          <title>Spending money, spending bytes</title>
      </head>
      <body>
          <p>Sic.</p>
      </body>
  </html>
  ```

  ```html
  <!-- 推荐 -->
  <!DOCTYPE html>
      <title>Saving money, saving bytes</title>
      <p>Qed.
  ```

  <a name="type-propertys" /><a name="4.8"></a>
  - [4.8](#type-propertys) 类型属性`type`: 样式表(style sheets)和脚本(scripts)元素省略`type`属性。

  > 不要给样式表使用`type`(除非用的不是CSS)，脚本也一样（除非用的不是Javascript)。
  > 指定`type`属性在HTML5的上下文环境中不是必须的，因为HTMl5隐式的将`text/css`和`text/javascript`作为默认值。即使在旧的浏览器中也可以安全运行。

  ```html
  <!-- 不推荐 -->
  <link rel="stylesheet" href="https://www.google.com/css/maia.css" type="text/css">

  <!-- 推荐 -->
  <link rel="stylesheet" href="https://www.google.com/css/maia.css">

  <!-- 不推荐 -->
  <script src="https://www.google.com/js/gweb/analytics/autotrack.js" type="text/javascript"></script>

  <!-- 推荐 -->
  <script src="https://www.google.com/js/gweb/analytics/autotrack.js"></script>
  ```

**[⬆ 顶部](#目录)**

### HTML格式化规则

  <a name="general-formatting" /><a name="5.1"></a>
  - [5.1](#document-type) 通用格式：给每个块，列表，表格元素另起一行，同时子元素进行缩进。

  > 独立于样式的元素(正如CSS允许元素扮演不同的角色通过`display`属性)，把每个块，列表，表格元素单起一行。
  > 同时，缩进它们如果它们是块，列表，表格的子元素。
  > （如果在列表项`li`之间遇到关于空白的问题，可以将所有li元素放在一行中。鼓励校验器发出警告而不是错误。）

  ```html
  <blockquote>
      <p><em>Space</em>, the final frontier.</p>
  </blockquote>

  <ul>
      <li>Moe
      <li>Larry
      <li>Curly
  </ul>

  <table>
      <thead>
          <tr>
              <th scope="col">Income
              <th scope="col">Taxes
      <tbody>
          <tr>
              <td>$ 5.00
              <td>$ 4.50
  </table>
  ```

  <a name="html-line-wrapping" /><a name="5.2"></a>
  - [5.2](#html-line-wrapping) HTML自动换行: 达到长行（可选的)。

  > 因为HTML没有推荐的列的限制，所以如果长行可以自动换行可以改善可读性，可以考虑。
  > 当换行时，每个后续的行相较原始行应该缩进2格。

  ```html
  <md-progress-circular md-mode="indeterminate" class="md-accent"
      ng-show="ctrl.loading" md-diameter="35">
  </md-progress-circular>

  <md-progress-circular
      md-mode="indeterminate"
      class="md-accent"
      ng-show="ctrl.loading"
      md-diameter="35">
  </md-progress-circular>

  <md-progress-circular md-mode="indeterminate"
      class="md-accent"
      ng-show="ctrl.loading"
      md-diameter="35">
  </md-progress-circular>
  ```

  <a name="html-quote-mark" /><a name="5.3"></a>
  - [5.3](#html-line-wrapping) HTML引号: 当引用属性值时，请用双引号。

  > 使用双引号`“”`而不是`单引号`包裹属性

  ```html
  <!-- 不推荐 -->
  <a class='maia-button maia-button-secondary'>Sign in</a>
  <!-- 推荐 -->
  <a class="maia-button maia-button-secondary">Sign in</a>
  ```

**[⬆ 顶部](#目录)**

## CSS规则

### CSS风格规则

  <a name="css-validity" /><a name="6.1"></a>
  - [6.1](#css-validity) CSS有效性: 在可能的地方使用有效的CSS。

  > 除非处理CSS校验器的bug或者需要合理的语法，否则使用有效的CSS代码。
  > 使用工具[W3C CSS 校验器] 来测试。
  > 使用有效的CSS是一个可测量的基线质量属性，它允许发现可能没有任何效果并且可以删除的CSS代码，并确保正确使用CSS。

  <a name="id-class-naming" /><a name="6.2"></a>
  - [6.2](#id-class-naming) 选择器ID和Class的命名: 使用有意义(meaningful)或者通用(generic)的id和类名。

  > 不要使用表示性的(presentational)或加密的名称，而是使用反映相关元素目的的名称，或者是通用的(generic)。
  > 名称具体明确(specific)且反映相关元素目的的名称是最易懂的，修改的可能性也最小。

  ```css
  /* 不推荐：无意义(meaningless) */
  #yee-1901 {}

  /* 不推荐：表示性的(presentational) */
  .button-green {}
  .clear {}

  /* 推荐：具体的明确的（specific) */
  #gallery {}
  #login {}
  .video {}

  /* 推荐：通用的(generic) */
  .aux {}
  .alt {}
  ```

  <a name="id-class-name-style" /><a name="6.3"></a>
  - [6.3](#id-class-name-style) 选择器ID和Class的命名风格: 使用尽可能短单必要的id和类名。

  > 尽量简短地传达一个ID或类是干什么的。
  > 使用上面的命名方式有助于提高代码信息的可接受性，可理解性，同时兼顾代码的效率。

  ```css
  /* 不推荐 */
  #navigation {}
  .atr {}

  /* 推荐 */
  #nav {}
  .author {}
  ```

  <a name="type-selectors" /><a name="6.4"></a>
  - [6.4](#type-selectors) 类型选择器: 避免使用类型选择器限定ID和类名。

  > 除非必须（比如辅助类),不要把元素名和ID或类名结合使用。
  > 出于[性能原因](http://www.stevesouders.com/blog/2009/06/18/simplifying-css-selectors/)避免使用非必须的祖先选择器，这非常有用。

  ```css
  /* 不推荐 */
  ul#example {}
  div.error {}

  /* 推荐 */
  #example {}
  .error {}
  ```

  <a name="shorthand-properties" /><a name="6.5"></a>
  - [6.5](#shorthand-properties) 属性缩写

  > 在可能的地方都使用属性缩写。
  > CSS提供了一序列的[属性缩写](https://www.w3.org/TR/CSS21/about.html#shorthand)（比如`font`）,在任何时候都要尽可能的使用，即使只有一个值要设置的情况也是。
  > 属性缩写有助于代码的效率和理解。

  ```css
  /* 不推荐 */
  border-top-style: none;
  font-family: palatino, georgia, serif;
  font-size: 100%;
  line-height: 1.6;
  padding-bottom: 2em;
  padding-left: 1em;
  padding-right: 1em;
  padding-top: 0;

  /* 推荐 */
  border-top: 0;
  font: 100%/1.6 palatino, georgia, serif;
  padding: 0 1em 2em;
  ```

  <a name="0-units" /><a name="6.6"></a>
  - [6.6](#type-selectors) 0和单位

  > 省略“0”值后面的单位规格，除非是必须的

  ```css
  flex: 0px; /* This flex-basis component requires a unit. */
  flex: 1 1 0px; /* Not ambiguous without the unit, but needed in IE11. */
  margin: 0;
  padding: 0;
  ```

  <a name="leading-0s" /><a name="6.7"></a>
  - [6.7](#leading-0s) 起首的0

  > 省略值中起首的"0"。
  > 不要把`0`放在值或者长度在-1和1的前面。

  ```css
  font-size: .8em;
  ```

  <a name="hexadecimal-notation" /><a name="6.8"></a>
  - [6.8](#hexadecimal-notation) 十六进制表示法

  > 在可能的地方，都使用3字符十六进制表示法
  > 对于允许它的颜色值，3个字符的十六进制表示法更短、更简洁。

  ```css
  /* 不推荐 */
  color: #eebbcc;

  /* 推荐 */
  color: #ebc;
  ```

  <a name="prefixs" /><a name="6.9"></a>
  - [6.9](#prefixs) 前缀

  > 为选择器添加特定于应用程序的前缀。
  > 在大型项目以及嵌入到其他项目或外部站点上的代码中，使用前缀（作为名称空间）来表示ID和类名。使用短的、唯一的标识符和破折号。
  > 使用名称空间有助于防止命名冲突，并且可以简化维护，例如在搜索和替换操作中。

  ```css
  .adw-help {} /* 广告语(AdWords) */
  #maia-note {} /* 玛雅(Maia) */
  ```

  <a name="id-class-name-delimiters" /><a name="6.10"></a>
  - [6.10](#id-class-name-delimiters) id和类命名时使用分隔符

  > ID和类名中的独立单词使用连字符连接
  > 为了提升理解性和可扫描性,不要使用连接符以外的其他字符（包括没有字符）来连接选择器中的单词和缩写

  ```css
  /* 不推荐： 没有分离“demo"和”image“单词 */
  .demoimage {}

  /* 不推荐： 使用下划线(_)而不是连接符(-) */
  .error_status {}

  /* 推荐 */
  #video-id {}
  .ads-sample {}
  ```

  <a name="hacks" /><a name="6.11"></a>
  - [6.11](#hacks) Hacks

  > 避免用户代理检测和CSS"hacks"-先尝试其它的方法。
  > 与用户代理检测或特殊的CSS过滤器、解决方法和黑客程序相比，解决样式差异是很有吸引力的。为了实现和维护一个有效且可管理的代码库，这两种方法都应该被视为最后的手段。另外，让检测和hacks没有代价的通过从长远来看会伤害项目，因为项目往往采取阻力最小的方式。也就是说，允许并使其易于使用检测和黑客意味着更频繁、更频繁地使用检测和黑客。(破窗效应)

### CSS格式化规则

  <a name="declaration-order" /><a name="7.1"></a>
  - [7.1](#declaration-order) 声明顺序：按字母排列顺序声明。

  > 把声明按字母顺序排列是为了实现一致的代码，这样易于记忆和维护。
  > 处于排序的目的忽略特定供应商的前缀。但是对于个供应商前缀进行排序(比如：-moz在-webkit之前)。

  ```css
  background: fuchsia;
  border: 1px solid;
  -moz-border-radius: 4px;
  -webkit-border-radius: 4px;
  border-radius: 4px;
  color: black;
  text-align: center;
  text-indent: 2em;
  ```

  <a name="block-content-indentation" /><a name="7.2"></a>
  - [7.2](#block-content-indentation) 块内容缩进：缩进所有块内容。

  > 缩进所有块内容，即规则和声明中的规则，以反映层次结构并提高理解。

  ```css
  @media screen, projection {

      html {
          background: #fff;
          color: #444;
      }

  }
  ```

  <a name="declaration-stops" /><a name="7.3"></a>
  - [7.3](#declaration-stops) 声明停止:使用分号在每个声明的最后。

  > 为了一致性和扩展性，使用分号结束每个声明。

  ```css
  /* 不推荐 */
  .test {
      display: block;
      height: 100px
  }

  /* 推荐 */
  .test {
      display: block;
      height: 100px;
  }
  ```

  <a name="property-name-stops" /><a name="7.4"></a>
  - [7.4](#declaration-stops) 属性名停止：使用一个空格咋属性名的冒号后面。

  > 因为一致性的原因,在属性和值之间，使用单个空格

  ```css
  /* 不推荐 */
  h3 {
      font-weight:bold;
  }

  /* 推荐 */
  h3 {
      font-weight: bold;
  }
  ```

  <a name="declaration-block-separation" /><a name="7.6"></a>
  - [7.6](#declaration-block-separation) 声明块分隔：在最后的选择器和声明块之间使用空格。

  > 始终在最好有一个选择器和开始快的左大括号之间使用一个空格。
  > 左大括号应与给定规则中的最后一个选择器同一行。

  ```css
  /* 不推荐: 空格缺失 */
  #video{
      margin-top: 1em;
  }

  /* 不推荐: 不需要的换行 */
  #video
  {
      margin-top: 1em;
  }

  /* 推荐 */
  #video {
      margin-top: 1em;
  }
  ```

  <a name="selector-declaration-separation" /><a name="7.7"></a>
  - [7.7](#selector-declaration-separation) 选择器和声明分离：用新行分隔选择器和声明。

  > 始终为每个选择器和声明开始一个新行。

  ```css
  /* 不推荐 */
  a:focus, a:active {
      position: relative; top: 1px;
  }

  /* 推荐 */
  h1,
  h2,
  h3 {
      font-weight: normal;
      line-height: 1.2;
  }
  ```

  <a name="rule-separation" /><a name="7.8"></a>
  - [7.8](#rule-separation) 规则分离：用新行分开规则。

  > 始终在规则之间放置一个空行(两个换行)。

  ```css
  html {
      background: #fff;
  }

  body {
      margin: auto;
      width: 50%;
  }
  ```

  <a name="css-quotation-mark" /><a name="7.9"></a>
  - [7.9](#css-quotation-mark) CSS引号：对属性选择器和属性值使用单引号(`''`)而不是双引号（`""`）。

  > 不要在URI值（`url()`）中使用引号。
  > 例外：如果确实需要使用`@charset`规则，请使用双引号-不允许使用[单引号](https://www.w3.org/TR/CSS21/syndata.html#charset).

  ```css
  /* 不推荐 */
  @import url("https://www.google.com/css/maia.css");

  html {
      font-family: "open sans", arial, sans-serif;
  }

  /* 推荐 */
  @import url(https://www.google.com/css/maia.css);

  html {
      font-family: 'open sans', arial, sans-serif;
  }
  ```

**[⬆ 顶部](#目录)**

### CSS元规则

  <a name="section-comments" /><a name="8.0"></a>
  - [8.0](#section-comments) 章节评论： 按章节注释（可选）对章节进行分组。

  > 如果可能，请使用注释将样式表章节祝贺在一起。使用新行分隔章节。

  ```css
  /* Header */

  #adw-header {}

  /* Footer */

  #adw-footer {}

  /* Gallery */

  .adw-gallery {}
  ```

**[⬆ 顶部](#目录)**

## 题外话

  > 始终如一(保持一致)。
  > 如果你正在编辑代码，请花几分钟时间查看你周围的代码并确定其风格。如果它们在所有运算符周围使用空格，那么你也应该这样做.如果他们的注释周围几乎没有哈希标记，那么让你的注释周围几乎没有哈希标记。
  > 拥有编码规范的关键是有一份共同的编码词汇表（通用术语），以便人们可以专注于你代码要说的信息，而不是你如何说。我们在这里介绍全局风格和规范，以便人们了解词汇表。但是具体文件已有的风格也很重要。如果你添加到文件中的代码看起来与他周围现有代买截然不同，那么当去阅读它时会使读者失去节奏，避免这样做。

**[⬆ 顶部](#目录)**