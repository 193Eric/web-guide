# 爱彼迎(Airbnb) JavaScript 样式风格() {

*A mostly reasonable approach to JavaScript*

> **注意事项**: 此规范预设你在使用 [Babel](https://babeljs.io), 以及使用 [babel-preset-airbnb](https://npmjs.com/babel-preset-airbnb) 或与之等价的库. 同时假设你在你的显目里安装了 shims/polyfills和 [airbnb-browser-shims](https://npmjs.com/airbnb-browser-shims) 或等价的库.

[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb.svg)](https://www.npmjs.com/package/eslint-config-airbnb)
[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb-base.svg)](https://www.npmjs.com/package/eslint-config-airbnb-base)
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/airbnb/javascript?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

本规范还有其它语言版本。参考[翻译](#translation)

其它样式规范
  - [英文github地址](https://github.com/airbnb/javascript)
  - [ES5 (Deprecated)](https://github.com/airbnb/javascript/tree/es5-deprecated/es5)
  - [React](react/)
  - [CSS-in-JavaScript](css-in-javascript/)
  - [CSS & Sass](https://github.com/airbnb/css)
  - [Ruby](https://github.com/airbnb/ruby)

## 内容索引

  1. [类型-Types](#类型-types)
  1. [参数-References](#参数-references)
  1. [对象-Objects](#对象-objects)
  1. [数组-Arrays](#数组-arrays)
  1. [解构-Destructuring](#解构-destructuring)
  1. [字符串-Strings](#字符串-strings)
  1. [函数-Functions](#函数-functions)
  1. [箭头函数-Arrow Functions](#箭头函数-arrow-functions)
  1. [类和构造器-Classes & Constructors](#类和构造器-classes--constructors)
  1. [模块化-Modules](#模块化-modules)
  1. [迭代器和生成器-Iterators and Generators](#迭代器和生成器-iterators-and-generators)
  1. [属性-Properties](#属性-properties)
  1. [变量-Variables](#变量-variables)
  1. [上升-Hoisting](#上升-hoisting)
  1. [比较运算符和等号-Comparison Operators & Equality](#比较运算符和等号-comparison-operators--equality)
  1. [块-Blocks](#块-blocks)
  1. [控制语句-Control Statements](#控制语句-control-statements)
  1. [注释-Comments](#注释-comments)
  1. [空格-Whitespace](#空格-whitespace)
  1. [逗号-Commas](#逗号-commas)
  1. [分号-Semicolons](#分号-semicolons)
  1. [强制类型转换-Type Casting & Coercion](#强制类型转换-type-casting--coercion)
  1. [命名习惯-Naming Conventions](#命名习惯-naming-conventions)
  1. [访问器-Accessors](#accessors)
  1. [事件-Events](#events)
  1. [jQuery](#jquery)
  1. [es5兼容-ECMAScript 5 Compatibility](#es5兼容-ecmascript-5-compatibility)
  1. [es6+风格-ECMAScript 6+ (ES 2015+) Styles](#es6+风格-ecmascript-6-es-2015-styles)
  1. [标准库-Standard Library](#标准库-standard-library)
  1. [测试-Testing](#测试-testing)
  1. [性能-Performance](#性能-performance)
  1. [资源-Resources](#资源-resources)
  1. [In the Wild](#in-the-wild)
  1. [Translation](#translation)
  1. [The JavaScript Style Guide Guide](#the-javascript-style-guide-guide)
  1. [Chat With Us About JavaScript](#chat-with-us-about-javascript)
  1. [Contributors](#contributors)
  1. [License](#license)
  1. [Amendments](#amendments)

## 类型-Types

  <a name="types--primitives" /><a name="1.1"></a>
  - [1.1](#types--primitives) **基本类型**: 当操作基本数据类型时直接操作它的值。

    - `string`
    - `number`
    - `boolean`
    - `null`
    - `undefined`
    - `symbol`

    ```javascript
    const foo = 1;
    let bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```

    - Symbols 无法完全polyfill, 所以它自能在非浏览器等原生支持的环境使用。

  <a name="types--complex" /><a name="1.2"></a>
  - [1.2](#types--complex)  **复杂类型**: 当你操作复杂类型时访问的通过引用来操作它的值。

    - `object`
    - `array`
    - `function`

    ```javascript
    const foo = [1, 2];
    const bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```

**[⬆ 顶部](#内容索引)**

## 标识符-References

  <a name="references--prefer-const" /><a name="2.1"></a>
  - [2.1](#references--prefer-const) 使用 `const` 声明你的标识符; 避免使用 `var`. eslint: [`prefer-const`](https://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign.html)

    > 为什么呢? 保证你不会重新赋值你的标识符, 这会导致bug和难以理解的代码。

    ```javascript
    // bad
    var a = 1;
    var b = 2;

    // good
    const a = 1;
    const b = 2;
    ```

  <a name="references--disallow-var" /><a name="2.2"></a>
  - [2.2](#references--disallow-var) 必须重新赋值的标识符，用`let`代替`var`. eslint: [`no-var`](https://eslint.org/docs/rules/no-var.html)

    > 为什么呢? `let` 是块级作用域（block-scoped）而`var`是函数作用域（function-scoped）。

    ```javascript
    // bad
    var count = 1;
    if (true) {
      count += 1;
    }

    // good, use the let.
    let count = 1;
    if (true) {
      count += 1;
    }
    ```

  <a name="references--block-scope" /><a name="2.3"></a>
  - [2.3](#references--block-scope) 注意： `let` 和 `const` 都是块级作用域(block-scoped)。

    ```javascript
    // const and let only exist in the blocks they are defined in.
    {
      let a = 1;
      const b = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
    ```

**[⬆ 顶部](#内容索引)**

## 对象-Objects

  <a name="objects--no-new" /><a name="3.1"></a>
  - [3.1](#objects--no-new) 使用字面量语法来定义对象。 eslint: [`no-new-object`](https://eslint.org/docs/rules/no-new-object.html)

    ```javascript
    // bad
    const item = new Object();

    // good
    const item = {};
    ```

  <a name="es6-computed-properties" /><a name="3.4"></a>
  - [3.2](#es6-computed-properties) 当创建的对象包含动态属性时用表达式定义属性名.

    > 为什么? 它们允许你在一个地方代码定义所有的属性.

    ```javascript
    // define fn
    function getKey(k) {
      return `a key named ${k}`;
    }

    // bad
    const obj = {
      id: 5,
      name: 'San Francisco',
    };
    obj[getKey('enabled')] = true;

    // good
    const obj = {
      id: 5,
      name: 'San Francisco',
      [getKey('enabled')]: true,
    };
    ```

  <a name="es6-object-shorthand" /><a name="3.5"></a>
  - [3.3](#es6-object-shorthand) 对象中定义的方法使用简洁表示法. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

    ```javascript
    // bad
    const atom = {
      value: 1,

      addValue: function (value) {
        return atom.value + value;
      },
    };

    // good
    const atom = {
      value: 1,

      addValue(value) {
        return atom.value + value;
      },
    };
    ```

  <a name="es6-object-concise" /><a name="3.6"></a>
  - [3.4](#es6-object-concise) 对象中属性使用简洁表示法. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

    > 为什么呢? 它更简洁更具描述属性.

    ```javascript
    const lukeSkywalker = 'Luke Skywalker';

    // bad
    const obj = {
      lukeSkywalker: lukeSkywalker,
    };

    // good
    const obj = {
      lukeSkywalker,
    };
    ```

  <a name="objects--grouped-shorthand" /><a name="3.7"></a>
  - [3.5](#objects--grouped-shorthand) 将简洁表示的属性组织在对象开始声明处.

    > 为什么呢? 它更容易区分那些属性使用了简洁表示法。

    ```javascript
    const anakinSkywalker = 'Anakin Skywalker';
    const lukeSkywalker = 'Luke Skywalker';

    // bad
    const obj = {
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      lukeSkywalker,
      episodeThree: 3,
      mayTheFourth: 4,
      anakinSkywalker,
    };

    // good
    const obj = {
      lukeSkywalker,
      anakinSkywalker,
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      episodeThree: 3,
      mayTheFourth: 4,
    };
    ```

  <a name="objects--quoted-props" /><a name="3.8"></a>
  - [3.6](#objects--quoted-props)引号仅用在无效的标识符作为属性时. eslint: [`quote-props`](https://eslint.org/docs/rules/quote-props.html)

    > 为什么? 一般情况下我们主观的认为这更易读。它优化了语法高亮同时更易被大多数JS引擎优化。

    ```javascript
    // bad
    const bad = {
      'foo': 3,
      'bar': 4,
      'data-blah': 5,
    };

    // good
    const good = {
      foo: 3,
      bar: 4,
      'data-blah': 5,
    };
    ```

  <a name="objects--prototype-builtins"></a>
  - [3.7](#objects--prototype-builtins) 禁止直接调用`Object.prototype`上的方法， 例如： `hasOwnProperty`, `propertyIsEnumerable`, and `isPrototypeOf`. eslint: [`no-prototype-builtins`](https://eslint.org/docs/rules/no-prototype-builtins)

    > 为什么? 在有问题的对象中这些方法可能被同名的属性遮挡了- 考虑下 `{ hasOwnProperty: false }` - 或者, 这个对象是一个`null`对象 (`Object.create(null)`).

    ```javascript
    // bad
    console.log(object.hasOwnProperty(key));

    // good
    console.log(Object.prototype.hasOwnProperty.call(object, key));

    // best
    const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
    /* or */
    import has from 'has'; // https://www.npmjs.com/package/has
    // ...
    console.log(has.call(object, key));
    ```

  <a name="objects--rest-spread"></a>
  - [3.8](#objects--rest-spread) 对象展开符优于[`Object.assign`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) 来进行浅拷贝对象. 使用对象 `rest` 运算符来获取一个没有枚举的属性组成的对象。

    ```javascript
    // very bad
    const original = { a: 1, b: 2 };
    const copy = Object.assign(original, { c: 3 }); // this mutates `original` ಠ_ಠ
    delete copy.a; // so does this

    // bad
    const original = { a: 1, b: 2 };
    const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

    // good
    const original = { a: 1, b: 2 };
    const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

    const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
    ```

**[⬆ 顶部](#内容索引)**

## 数组-Arrays

  <a name="arrays--literals"><a name="4.1"></a>
  - [4.1](#arrays--literals) 用字面量语法来定义数组. eslint: [`no-array-constructor`](https://eslint.org/docs/rules/no-array-constructor.html)

    ```javascript
    // bad
    const items = new Array();

    // good
    const items = [];
    ```

  <a name="arrays--push"></a><a name="4.2"></a>
  - [4.2](#arrays--push) 用 [Array#push](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push) 代替直接赋值来添加数组元素

    ```javascript
    const someStack = [];

    // bad
    someStack[someStack.length] = 'abracadabra';

    // good
    someStack.push('abracadabra');
    ```

  <a name="es6-array-spreads"></a><a name="4.3"></a>
  - [4.3](#es6-array-spreads) 用数组展开符`...`来拷贝数组。

    ```javascript
    // bad
    const len = items.length;
    const itemsCopy = [];
    let i;

    for (i = 0; i < len; i += 1) {
      itemsCopy[i] = items[i];
    }

    // good
    const itemsCopy = [...items];
    ```

  <a name="arrays--from"></a>
  <a name="arrays--from-iterable"></a><a name="4.4"></a>
  - [4.4](#arrays--from-iterable) 使用展开符`...`代替[`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from)将可迭代对象转化为数组

    ```javascript
    const foo = document.querySelectorAll('.foo');

    // good
    const nodes = Array.from(foo);

    // best
    const nodes = [...foo];
    ```

  <a name="arrays--from-array-like"></a>
  - [4.5](#arrays--from-array-like) 使用 [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) 将伪数组(array-like)对象转化成数组。

    ```javascript
    const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };

    // bad
    const arr = Array.prototype.slice.call(arrLike);

    // good
    const arr = Array.from(arrLike);
    ```

  <a name="arrays--mapping"></a>
  - [4.6](#arrays--mapping) 用 [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) 代替展开符`...`和map方法来将想要转换成数组的维数组或可迭代对象,因为可以避免创建一个中间数组。

    ```javascript
    // bad
    const baz = [...foo].map(bar);

    // good
    const baz = Array.from(foo, bar);
    ```

  <a name="arrays--callback-return"></a><a name="4.5"></a>
  - [4.7](#arrays--callback-return) 在数组原生方法的回调函数参数要使用`return`语句返回指定语句。 在回调函数体只由单一语句组成时可以忽略`return`语句，不会有副作用。 参考 [8.2](#arrows--implicit-return). eslint: [`array-callback-return`](https://eslint.org/docs/rules/array-callback-return)

    ```javascript
    // good
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });

    // good
    [1, 2, 3].map(x => x + 1);

    // bad - no returned value means `acc` becomes undefined after the first iteration
    [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
      const flatten = acc.concat(item);
      acc[index] = flatten;
    });

    // good
    [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
      const flatten = acc.concat(item);
      acc[index] = flatten;
      return flatten;
    });

    // bad
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      } else {
        return false;
      }
    });

    // good
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      }

      return false;
    });
    ```

  <a name="arrays--bracket-newline"></a>
  - [4.8](#arrays--bracket-newline) 当数组有多行时，在数组括号的开始和结束处换行。

    ```javascript
    // bad
    const arr = [
      [0, 1], [2, 3], [4, 5],
    ];

    const objectInArray = [{
      id: 1,
    }, {
      id: 2,
    }];

    const numberInArray = [
      1, 2,
    ];

    // good
    const arr = [[0, 1], [2, 3], [4, 5]];

    const objectInArray = [
      {
        id: 1,
      },
      {
        id: 2,
      },
    ];

    const numberInArray = [
      1,
      2,
    ];
    ```

**[⬆ 顶部](#内容索引)**

## 解构-Destructuring

  <a name="destructuring--object" /><a name="5.1"></a>
  - [5.1](#destructuring--object) 使用对象结构来访问一个对象中的多个属性。eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    > 为什么呢?解构精简了临时变量的创建。

    ```javascript
    // bad
    function getFullName(user) {
      const firstName = user.firstName;
      const lastName = user.lastName;

      return `${firstName} ${lastName}`;
    }

    // good
    function getFullName(user) {
      const { firstName, lastName } = user;
      return `${firstName} ${lastName}`;
    }

    // best
    function getFullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    }
    ```

  <a name="destructuring--array" /><a name="5.2"></a>
  - [5.2](#destructuring--array) 在可以的地方使用数组解构。 eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    ```javascript
    const arr = [1, 2, 3, 4];

    // bad
    const first = arr[0];
    const second = arr[1];

    // good
    const [first, second] = arr;
    ```

  <a name="destructuring--object-over-array" /><a name="5.3"></a>
  - [5.3](#destructuring--object-over-array) 多个返回值使用对象解构优于数组解构。

    > 为什么呢? 在你添加新的属性，或改变属性的位置时不用修改调用这些值的代码。

    ```javascript
    // bad
    function processInput(input) {
      // then a miracle occurs
      return [left, right, top, bottom];
    }

    // the caller needs to think about the order of return data
    const [left, __, top] = processInput(input);

    // good
    function processInput(input) {
      // then a miracle occurs
      return { left, right, top, bottom };
    }

    // the caller selects only the data they need
    const { left, top } = processInput(input);
    ```

**[⬆ 顶部](#table-of-contents)**

## 字符串-Strings

  <a name="strings--quotes" /><a name="6.1"></a>
  - [6.1](#strings--quotes) 字符串使用单引号。 eslint: [`quotes`](https://eslint.org/docs/rules/quotes.html)

    ```javascript
    // bad
    const name = "Capt. Janeway";

    // bad - template literals should contain interpolation or newlines
    const name = `Capt. Janeway`;

    // good
    const name = 'Capt. Janeway';
    ```

  <a name="strings--line-length" /><a name="6.2"></a>
  - [6.2](#strings--line-length) 字符串导致行框超过100字符不要用多行连接符`\`或用`+`拼接字符串。

    > 为什么? 截断字符串是痛苦的，同时不利于文本搜索。

    ```javascript
    // bad
    const errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // bad
    const errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';

    // good
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
    ```

  <a name="es6-template-literals" /><a name="6.4"></a>
  - [6.3](#es6-template-literals) 当使用程序构建字符串时使用模板，代替拼接。eslint: [`prefer-template`](https://eslint.org/docs/rules/prefer-template.html) [`template-curly-spacing`](https://eslint.org/docs/rules/template-curly-spacing)

    > 为什么呢? 模板带来可读性，通过简洁的语法以合理的换行以及字符串插值特性。

    ```javascript
    // bad
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }

    // bad
    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
    }

    // bad
    function sayHi(name) {
      return `How are you, ${ name }?`;
    }

    // good
    function sayHi(name) {
      return `How are you, ${name}?`;
    }
    ```

  <a name="strings--eval" /><a name="6.5"></a>
  - [6.4](#strings--eval) 绝对不要使用 `eval()` 来处理字符串, 它打开了太多漏洞。eslint: [`no-eval`](https://eslint.org/docs/rules/no-eval)

  <a name="strings--escaping"></a>
  - [6.5](#strings--escaping) 不对非必须转义的字符串进行转义。 eslint: [`no-useless-escape`](https://eslint.org/docs/rules/no-useless-escape)

    > 为什么呢? 反斜杠伤害可读性, 因此它们只在需要的时候出现。

    ```javascript
    // bad
    const foo = '\'this\' \i\s \"quoted\"';

    // good
    const foo = '\'this\' is "quoted"';
    const foo = `my name is '${name}'`;
    ```

**[⬆ 顶部](#内容索引)**

## 函数-Functions

  <a name="functions--declarations" /><a name="7.1"></a>
  - [7.1](#functions--declarations) 使用命名函数表达式代替函数声明。 eslint: [`func-style`](https://eslint.org/docs/rules/func-style)

    > 为什么呢? 函数声明会引起提升(hoisted),这意味着容易-很容易-在函数定义在文件之前调用这个函数。这伤害了可读性和维护性。如果你发现一个函数的定义巨大或者复杂到影响了文件剩余部分的理解，那么也许是时候将它抽取到一个独立的模块中了。别忘了显式的命名函数表达式，不管这名字是否是从包含的变量推到出来的（在现代浏览器或者使用Babel编译器这种情况经常出现）。这可以消除错误调用栈的任何假设。([Discussion](https://github.com/airbnb/javascript/issues/794))

    ```javascript
    // bad
    function foo() {
      // ...
    }

    // bad
    const foo = function () {
      // ...
    };

    // good
    // lexical name distinguished from the variable-referenced invocation(s)
    const short = function longUniqueMoreDescriptiveLexicalFoo() {
      // ...
    };
    ```

  <a name="functions--iife" /><a name="7.2"></a>
  - [7.2](#functions--iife) 用括号包裹立即调用函数表达式。 eslint: [`wrap-iife`](https://eslint.org/docs/rules/wrap-iife.html)

    > 为什么呢? 立即调用函数表达式(IIFE)是一个独立的单元-包括函数自己和它的调用括号，都在括号里面，清晰的表单这些。注意在一切皆模块的世界，你几乎用不上IIFE.

    ```javascript
    // immediately-invoked function expression (IIFE)
    (function () {
      console.log('Welcome to the Internet. Please follow me.');
    }());
    ```

  <a name="functions--in-blocks" /><a name="7.3"></a>
  - [7.3](#functions--in-blocks) 不用在非函数块中声明函数(`if`, `while`, etc). 通过把函数赋值给变量来实现。虽然浏览器允许,但是坏消息是，不同浏览器之间编译代码有差异。 eslint: [`no-loop-func`](https://eslint.org/docs/rules/no-loop-func.html)

  <a name="functions--note-on-blocks" /><a name="7.4"></a>
  - [7.4](#functions--note-on-blocks) **注意:** ECMA-262 将块`block`定义为一系列语句的组合。 函数声明不是语句。

    ```javascript
    // bad
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // good
    let test;
    if (currentUser) {
      test = () => {
        console.log('Yup.');
      };
    }
    ```

  <a name="functions--arguments-shadow" /><a name="7.5"></a>
  - [7.5](#functions--arguments-shadow) 不要使用`arguments`作为参数。它将覆盖默认给到函数作用域的`arguments`对象。

    ```javascript
    // bad
    function foo(name, options, arguments) {
      // ...
    }

    // good
    function foo(name, options, args) {
      // ...
    }
    ```

  <a name="es6-rest"/><a name="7.6"></a>
  - [7.6](#es6-rest) 不要使用`arguments`参数，使用剩余操作符 `...`。 eslint: [`prefer-rest-params`](https://eslint.org/docs/rules/prefer-rest-params)

    > 为什么呢? `...`显式的表示你想推入的参数。另外，剩余操作符，是一个真数组而`arguments`是维数组。

    ```javascript
    // bad
    function concatenateAll() {
      const args = Array.prototype.slice.call(arguments);
      return args.join('');
    }

    // good
    function concatenateAll(...args) {
      return args.join('');
    }
    ```

  <a name="es6-default-parameters"></a><a name="7.7"></a>
  - [7.7](#es6-default-parameters) 使用默认参数语法而不是改变函数参数。

    ```javascript
    // really bad
    function handleThings(opts) {
      // No! We shouldn’t mutate function arguments.
      // 禁止！我们不应该改变函数参数
      // Double bad: if opts is falsy it'll be set to an object which may
      // 双倍的坏味道：如果`opts`是假值（falsy）,将它设为空对象是你设想的，但是可能引入微妙的bugs。
      // be what you want but it can introduce subtle bugs.
      opts = opts || {};
      // ...
    }

    // still bad
    function handleThings(opts) {
      if (opts === void 0) { // `void 0` 是更安全的获得 undefined 的方法
        opts = {};
      }
      // ...
    }

    // good
    function handleThings(opts = {}) {
      // ...
    }
    ```

  <a name="functions--default-side-effects" /><a name="7.8"></a>
  - [7.8](#functions--default-side-effects) 避免默认参数的副作用。

    > 为什么呢? 它们使得推算混乱不清。

    ```javascript
    var b = 1;
    // bad
    function count(a = b++) {
      console.log(a);
    }
    count();  // 1
    count();  // 2
    count(3); // 3
    count();  // 3
    ```

  <a name="functions--defaults-last" /><a name="7.9"></a>
  - [7.9](#functions--defaults-last) 总是在把默认参数放在最后。

    ```javascript
    // bad
    function handleThings(opts = {}, name) {
      // ...
    }

    // good
    function handleThings(name, opts = {}) {
      // ...
    }
    ```

  <a name="functions--constructor" /><a name="7.10"></a>
  - [7.10](#functions--constructor) 绝不使用函数构造函数创建一个新的函数。 eslint: [`no-new-func`](https://eslint.org/docs/rules/no-new-func)

    > 为什么呢? 使用上面的方式创建函数类似于用`eval()`执行字符串,这会打开许多漏洞。

    ```javascript
    // bad
    var add = new Function('a', 'b', 'return a + b');

    // still bad
    var subtract = Function('a', 'b', 'return a - b');
    ```

  <a name="functions--signature-spacing" /><a name="7.11"></a>
  - [7.11](#functions--signature-spacing) 分隔函数签名(关键字和参数)。 eslint: [`space-before-function-paren`](https://eslint.org/docs/rules/space-before-function-paren) [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks)

    > 为什么呢? 保持一致性是好的习惯，同时你添加或者删除名称时不用操作空格。

    ```javascript
    // bad
    const f = function(){};
    const g = function (){};
    const h = function() {};

    // good
    const x = function () {};
    const y = function a() {};
    ```

  <a name="functions--mutate-params" /><a name="7.12"></a>
  - [7.12](#functions--mutate-params) 不允许修改函数的参数. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)

    > 为什么呢? 当操作作为参数的对象时可能在原始对象中导致意想不到的变量副作用。

    ```javascript
    // bad
    function f1(obj) {
      obj.key = 1;
    }

    // good
    function f2(obj) {
      const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
    }
    ```

  <a name="functions--reassign-params" /><a name="7.13"></a>
  - [7.13](#functions--reassign-params) 不允许重新赋值参数。 eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)

    > 为什么? 重新赋值参数可能导致非预期的行为，特别当访问`arguments`对象。还会导致优化问题，特别是v8引擎中。

    ```javascript
    // bad
    function f1(a) {
      a = 1;
      // ...
    }

    function f2(a) {
      if (!a) { a = 1; }
      // ...
    }

    // good
    function f3(a) {
      const b = a || 1;
      // ...
    }

    function f4(a = 1) {
      // ...
    }
    ```

  <a name="functions--spread-vs-apply" /><a name="7.14"></a>
  - [7.14](#functions--spread-vs-apply) 使用扩展运算符`...` 调用可变函数(参数不确定)是更好的习惯。eslint: [`prefer-spread`](https://eslint.org/docs/rules/prefer-spread)

    > 为什么? 更清晰，不用设定上执行上下文。同时法简洁的组织`new`和`apply`。

    ```javascript
    // bad
    const x = [1, 2, 3, 4, 5];
    console.log.apply(console, x);

    // good
    const x = [1, 2, 3, 4, 5];
    console.log(...x);

    // bad
    new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

    // good
    new Date(...[2016, 8, 5]);
    ```

  <a name="functions--signature-invocation-indentation"></a>
  - [7.15](#functions--signature-invocation-indentation) 多行签名的函数或者函数调用，应该和这份规范中的其它多行一样缩进: 每一项单独一行，逗号在每一行的结尾。 eslint: [`function-paren-newline`](https://eslint.org/docs/rules/function-paren-newline)

    ```javascript
    // bad
    function foo(bar,
                 baz,
                 quux) {
      // ...
    }

    // good
    function foo(
      bar,
      baz,
      quux,
    ) {
      // ...
    }

    // bad
    console.log(foo,
      bar,
      baz);

    // good
    console.log(
      foo,
      bar,
      baz,
    );
    ```

**[⬆ 顶部](#内容索引)**

## 箭头函数-Arrow Functions

  <a name="arrows--use-them" /><a name="8.1"></a>
  - [8.1](#arrows--use-them) 单必须使用匿名函数时(例如：内联的回调函数)使用箭头函数符号。 eslint: [`prefer-arrow-callback`](https://eslint.org/docs/rules/prefer-arrow-callback.html), [`arrow-spacing`](https://eslint.org/docs/rules/arrow-spacing.html)

    > 为什么呢? 它创建的函数执行作用域`this`通常是你需要的，同时语法更简洁。
    > 什么时候不呢? 如果你有一个相当复杂的函数，你也许应该将这部分逻辑移动到拥有命名的函数表达式中。

    ```javascript
    // bad
    [1, 2, 3].map(function (x) {
      const y = x + 1;
      return x * y;
    });

    // good
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--implicit-return" /><a name="8.2"></a>
  - [8.2](#arrows--implicit-return) 如果函数体是由单一返回语句组成的[表达式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions) 没有副作用,省略括号和`return`关键字使用隐式返回。 否则保留括号使用`return`语句。 eslint: [`arrow-parens`](https://eslint.org/docs/rules/arrow-parens.html), [`arrow-body-style`](https://eslint.org/docs/rules/arrow-body-style.html)

    > 为什么呢? 语法糖。当多个函数链式调用时可读性佳。

    ```javascript

    // bad
    [1, 2, 3].map(number => {
      const nextNumber = number + 1;
      `A string containing the ${nextNumber}.`;
    });

    // good
    [1, 2, 3].map(number => `A string containing the ${number}.`);

    // good
    [1, 2, 3].map((number) => {
      const nextNumber = number + 1;
      return `A string containing the ${nextNumber}.`;
    });

    // good
    [1, 2, 3].map((number, index) => ({
      [index]: number,
    }));

    // No implicit return with side effects
    function foo(callback) {
      const val = callback();
      if (val === true) {
        // Do something if callback returns true
      }
    }

    let bool = false;

    // bad
    foo(() => bool = true);

    // good
    foo(() => {
      bool = true;
    });

    ```

  <a name="arrows--paren-wrap" /><a name="8.3"></a>
  - [8.3](#arrows--paren-wrap) 如果表达式跨越多行,使用圆括号包裹，更具可读性。

    > 为什么呢? 这清晰的表明了函数的的开始和结束在哪里。

    ```javascript
    // bad
    ['get', 'post', 'put'].map(httpMethod => Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
      )
    );

    // good
    ['get', 'post', 'put'].map(httpMethod => (
      Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
      )
    ));
    ```

  <a name="arrows--one-arg-parens" /><a name="8.4"></a>
  - [8.4](#arrows--one-arg-parens) 当函数只有单一参数且函数体没有花括号时，省略包裹参数的括号。 否则，参数需要带着括号，来保持清晰和一致性。 注意: 也可以接受括号总是使用括号,在那些eslint设置了["always" 选项](https://eslint.org/docs/rules/arrow-parens#always) 的项目里。 eslint: [`arrow-parens`](https://eslint.org/docs/rules/arrow-parens.html)

    > 为什么呢? 减少视觉的杂乱。

    ```javascript
    // bad
    [1, 2, 3].map((x) => x * x);

    // good
    [1, 2, 3].map(x => x * x);

    // good
    [1, 2, 3].map(number => (
      `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
    ));

    // bad
    [1, 2, 3].map(x => {
      const y = x + 1;
      return x * y;
    });

    // good
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--confusing" /><a name="8.5"></a>
  - [8.5](#arrows--confusing) 避免箭头函数语法(`=>`)与比较操作符(`<=`,`>=`)带来的混乱。eslint: [`no-confusing-arrow`](https://eslint.org/docs/rules/no-confusing-arrow)

    ```javascript
    // bad
    const itemHeight = item => item.height <= 256 ? item.largeSize : item.smallSize;

    // bad
    const itemHeight = (item) => item.height >= 256 ? item.largeSize : item.smallSize;

    // good
    const itemHeight = item => (item.height <= 256 ? item.largeSize : item.smallSize);

    // good
    const itemHeight = (item) => {
      const { height, largeSize, smallSize } = item;
      return height <= 256 ? largeSize : smallSize;
    };
    ```

  <a name="whitespace--implicit-arrow-linebreak"></a>
  - [8.6](#whitespace--implicit-arrow-linebreak) 强制带有隐式返回的箭头函数体的位置。eslint: [`implicit-arrow-linebreak`](https://eslint.org/docs/rules/implicit-arrow-linebreak)

    ```javascript
    // bad
    foo =>
      bar;

    foo =>
      (bar);

    // good
    foo => bar;
    foo => (bar);
    foo => (
      bar
    )
    ```

**[⬆ 顶部](#内容索引)**

## 类和构造器-Classes & Constructors

  <a name="constructors--use-class" /><a name="9.1"></a>
  - [9.1](#constructors--use-class) 总是使用关键字`class`。避免直接操作原型链`prototype`。

    > 为什么呢? `class` 语法更简洁和易于推断。

    ```javascript
    // bad
    function Queue(contents = []) {
      this.queue = [...contents];
    }
    Queue.prototype.pop = function () {
      const value = this.queue[0];
      this.queue.splice(0, 1);
      return value;
    };

    // good
    class Queue {
      constructor(contents = []) {
        this.queue = [...contents];
      }
      pop() {
        const value = this.queue[0];
        this.queue.splice(0, 1);
        return value;
      }
    }
    ```

  <a name="constructors--extends" /><a name="9.2"></a>
  - [9.2](#constructors--extends) 使用 `extends` 关键字来实现继承.

    > 为什么呢? 这是内建的（buit-in）继承原型链的功能不会破坏`instanceof`关键字。

    ```javascript
    // bad
    const inherits = require('inherits');
    function PeekableQueue(contents) {
      Queue.apply(this, contents);
    }
    inherits(PeekableQueue, Queue);
    PeekableQueue.prototype.peek = function () {
      return this.queue[0];
    };

    // good
    class PeekableQueue extends Queue {
      peek() {
        return this.queue[0];
      }
    }
    ```

  <a name="constructors--chaining" /><a name="9.3"></a>
  - [9.3](#constructors--chaining) 方法可以放回`this`来帮助实现链式调用。

    ```javascript
    // bad
    Jedi.prototype.jump = function () {
      this.jumping = true;
      return true;
    };

    Jedi.prototype.setHeight = function (height) {
      this.height = height;
    };

    const luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight(20); // => undefined

    // good
    class Jedi {
      jump() {
        this.jumping = true;
        return this;
      }

      setHeight(height) {
        this.height = height;
        return this;
      }
    }

    const luke = new Jedi();

    luke.jump()
      .setHeight(20);
    ```

  <a name="constructors--tostring" /><a name="9.4"></a>
  - [9.4](#constructors--tostring) 可以重写`toString()`方法，但需要保证它能正确工作，同时没有副作用。

    ```javascript
    class Jedi {
      constructor(options = {}) {
        this.name = options.name || 'no name';
      }

      getName() {
        return this.name;
      }

      toString() {
        return `Jedi - ${this.getName()}`;
      }
    }
    ```

  <a name="constructors--no-useless" /><a name="9.5"></a>
  - [9.5](#constructors--no-useless) 类有一个默认的构造器，如果没有特别指定的话。一个空的构造函数，或者只是委托职责给父类不是必需的。 eslint: [`no-useless-constructor`](https://eslint.org/docs/rules/no-useless-constructor)

    ```javascript
    // bad
    class Jedi {
      constructor() {}

      getName() {
        return this.name;
      }
    }

    // bad
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
      }
    }

    // good
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
        this.name = 'Rey';
      }
    }
    ```

  <a name="classes--no-duplicate-members"></a>
  - [9.6](#classes--no-duplicate-members) 避免重复定义类的成员。 eslint: [`no-dupe-class-members`](https://eslint.org/docs/rules/no-dupe-class-members)

    > 为什么呢? 重复的类成员将静默的使用后面的定义（没有提示）- 这几乎肯定会引入bug。

    ```javascript
    // bad
    class Foo {
      bar() { return 1; }
      bar() { return 2; }
    }

    // good
    class Foo {
      bar() { return 1; }
    }

    // good
    class Foo {
      bar() { return 2; }
    }
    ```

**[⬆ 顶部](#内容索引)**

## 模块化-Modules

  <a name="modules--use-them" /><a name="10.1"></a>
  - [10.1](#modules--use-them) 总是使用标准的模块系统（`import`/`export`。

    > 为什么? 模块化时趋势，重现在就开始吧。

    ```javascript
    // bad
    const AirbnbStyleGuide = require('./AirbnbStyleGuide');
    module.exports = AirbnbStyleGuide.es6;

    // ok
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    export default AirbnbStyleGuide.es6;

    // best
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-wildcard" /><a name="10.2"></a>
  - [10.2](#modules--no-wildcard) 禁止使用通配符引入模块。

    > 为什么呢? 这确保只有唯一一个默认的输出。

    ```javascript
    // bad
    import * as AirbnbStyleGuide from './AirbnbStyleGuide';

    // good
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    ```

  <a name="modules--no-export-from-import" /><a name="10.3"></a>
  - [10.3](#modules--no-export-from-import) 禁止直接输出一个输入。

    > 为什么呢? 虽然只有一行很简洁，但是有一个明确的输入和一个明确的输出，语义更清晰。

    ```javascript
    // bad
    // filename es6.js
    export { es6 as default } from './AirbnbStyleGuide';

    // good
    // filename es6.js
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-duplicate-imports"></a>
  - [10.4](#modules--no-duplicate-imports) 一个模块有且仅有一个地方输入。
 eslint: [`no-duplicate-imports`](https://eslint.org/docs/rules/no-duplicate-imports)
    > 为什么? 有多行输入来自同一个模块，使得代码难以维护。

    ```javascript
    // bad
    import foo from 'foo';
    // … some other imports … //
    import { named1, named2 } from 'foo';

    // good
    import foo, { named1, named2 } from 'foo';

    // good
    import foo, {
      named1,
      named2,
    } from 'foo';
    ```

  <a name="modules--no-mutable-exports"></a>
  - [10.5](#modules--no-mutable-exports) 禁止输出可变的绑定。
 eslint: [`import/no-mutable-exports`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-mutable-exports.md)
    > 为什么? 变化通常应该避免，特别是输出的绑定。当然技术上也许会有一些特例，但是一般情况只有常量引用可以被输出。

    ```javascript
    // bad
    let foo = 3;
    export { foo };

    // good
    const foo = 3;
    export { foo };
    ```

  <a name="modules--prefer-default-export"></a>
  - [10.6](#modules--prefer-default-export) 只有单一输出的模块,使用默认输出优于命名输出。
 eslint: [`import/prefer-default-export`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/prefer-default-export.md)
    > 为什么呢? 目的是为了鼓励更多的文件只输出一个结果，这更利于阅读和维护。

    ```javascript
    // bad
    export function foo() {}

    // good
    export default function foo() {}
    ```

  <a name="modules--imports-first"></a>
  - [10.7](#modules--imports-first) 把所有`import`语句置于非import语句之前。
 eslint: [`import/first`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/first.md)
    > 为什么呢? 因为 `import` 语句具有上升的特性(hoisted)，将它们置于顶部避免意外的行为。

    ```javascript
    // bad
    import foo from 'foo';
    foo.init();

    import bar from 'bar';

    // good
    import foo from 'foo';
    import bar from 'bar';

    foo.init();
    ```

  <a name="modules--multiline-imports-over-newlines"></a>
  - [10.8](#modules--multiline-imports-over-newlines) 多行输入应该缩进与多行数组，多行对象字面量一样。

    > 为什么呢? 花括号与这份规范其它说明花括号的地方的缩进规则保持一致，尾部的逗号规则也是一样的。

    ```javascript
    // bad
    import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';

    // good
    import {
      longNameA,
      longNameB,
      longNameC,
      longNameD,
      longNameE,
    } from 'path';
    ```

  <a name="modules--no-webpack-loader-syntax"></a>
  - [10.9](#modules--no-webpack-loader-syntax) 模块映入语句中不允许Webpack 加载器语法
 eslint: [`import/no-webpack-loader-syntax`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-webpack-loader-syntax.md)
    > 为什么呢? 因为Webpack语法引入了把代码连接到了打包的模块。更好的方式是把加载器语法定义在配置文件中（`webpack.config.js`)。

    ```javascript
    // bad
    import fooSass from 'css!sass!foo.scss';
    import barCss from 'style!css!bar.css';

    // good
    import fooSass from 'foo.scss';
    import barCss from 'bar.css';
    ```

**[⬆ 顶部](#内容索引)**

## 迭代器和生成器-Iterators and Generators

  <a name="iterators--nope" /><a name="11.1"></a>
  - [11.1](#iterators--nope) 不要使用迭代器。 使用Javascript 的高阶函数来代替`for-in`或者 `for-of`。eslint: [`no-iterator`](https://eslint.org/docs/rules/no-iterator.html) [`no-restricted-syntax`](https://eslint.org/docs/rules/no-restricted-syntax)

    > 问什么呢? 这强迫我们遵循不变的规则。相较于处理返回值，纯函数更易于推测和掌控它的副作用。

    > 使用 `map()` / `every()` / `filter()` / `find()` / `findIndex()` / `reduce()` / `some()` / ... 来迭代数组, 同时 `Object.keys()` / `Object.values()` / `Object.entries()` 来生成数组以便你能迭代对象。

    ```javascript
    const numbers = [1, 2, 3, 4, 5];

    // bad
    let sum = 0;
    for (let num of numbers) {
      sum += num;
    }
    sum === 15;

    // good
    let sum = 0;
    numbers.forEach((num) => {
      sum += num;
    });
    sum === 15;

    // best (use the functional force)
    const sum = numbers.reduce((total, num) => total + num, 0);
    sum === 15;

    // bad
    const increasedByOne = [];
    for (let i = 0; i < numbers.length; i++) {
      increasedByOne.push(numbers[i] + 1);
    }

    // good
    const increasedByOne = [];
    numbers.forEach((num) => {
      increasedByOne.push(num + 1);
    });

    // best (keeping it functional)
    const increasedByOne = numbers.map(num => num + 1);
    ```

  <a name="generators--nope" /><a name="11.2"></a>
  - [11.2](#generators--nope) 不要使用生成器,从现在开始。

    > 为什么呢? 它们对ES5的兼容性不友好。They don’t transpile well to ES5.

  <a name="generators--spacing"></a>
  - [11.3](#generators--spacing) 如果你必需使用生成器，或者你忽视[我们的建议](#generators--nope), 确保它们的函数签名被合理分隔。 eslint: [`generator-star-spacing`](https://eslint.org/docs/rules/generator-star-spacing)

    > 为什么呢? `function` 和 `*` 是相同概念上的关键字的两个部分 - `*` 不是 `function`的修饰符, `function*` 是一个唯一的结构和 `function`是不同的.

    ```javascript
    // bad
    function * foo() {
      // ...
    }

    // bad
    const bar = function * () {
      // ...
    };

    // bad
    const baz = function *() {
      // ...
    };

    // bad
    const quux = function*() {
      // ...
    };

    // bad
    function*foo() {
      // ...
    }

    // bad
    function *foo() {
      // ...
    }

    // very bad
    function
    *
    foo() {
      // ...
    }

    // very bad
    const wat = function
    *
    () {
      // ...
    };

    // good
    function* foo() {
      // ...
    }

    // good
    const foo = function* () {
      // ...
    };
    ```

**[⬆ 顶部](#内容索引)**

## 属性-Properties

  <a name="properties--dot" /><a name="12.1"></a>
  - [12.1](#properties--dot) 使用点运算符(`.`)访问属性。 eslint: [`dot-notation`](https://eslint.org/docs/rules/dot-notation.html)

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    // bad
    const isJedi = luke['jedi'];

    // good
    const isJedi = luke.jedi;
    ```

  <a name="properties--bracket" /><a name="12.2"></a>
  - [12.2](#properties--bracket) 当使用变量访问属性时使用中括号运算符（`[]`）。

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    function getProp(prop) {
      return luke[prop];
    }

    const isJedi = getProp('jedi');
    ```
  <a name="es2016-properties--exponentiation-operator"></a>
  - [12.3](#es2016-properties--exponentiation-operator) 进行幂运算时使用幂运算操作符 `**`。eslint: [`no-restricted-properties`](https://eslint.org/docs/rules/no-restricted-properties).

    ```javascript
    // bad
    const binary = Math.pow(2, 10);

    // good
    const binary = 2 ** 10;
    ```

**[⬆ 顶部](#内容索引)**

## 变量-Variables

  <a name="variables--const" /><a name="13.1"></a>
  - [13.1](#variables--const) 总是使用 `const` 或 `let` 来声明变量。 不加关键字声明将导致全局变量。 我们要避免污染全局命名空间。 eslint: [`no-undef`](https://eslint.org/docs/rules/no-undef) [`prefer-const`](https://eslint.org/docs/rules/prefer-const)

    ```javascript
    // bad
    superPower = new SuperPower();

    // good
    const superPower = new SuperPower();
    ```

  <a name="variables--one-const" /><a name="13.2"></a>
  - [13.2](#variables--one-const) 每个`const`或`let`与变量或赋值一一对应. eslint: [`one-var`](https://eslint.org/docs/rules/one-var.html)

    > 为什么呢? 便于添加行的变量声明，同时不必关注结尾使用`;`还是`,`。你也可以再每个声明上进行单步调试，而不会一次跳过全部。

    ```javascript
    // bad
    const items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

    // bad
    // (compare to above, and try to spot the mistake)
    const items = getItems(),
        goSportsTeam = true;
        dragonball = 'z';

    // good
    const items = getItems();
    const goSportsTeam = true;
    const dragonball = 'z';
    ```

  <a name="variables--const-let-group" /><a name="13.3"></a>
  - [13.3](#variables--const-let-group) 将所用`const`归为一组，同时所有`let`归为一组。

    > 为什么呢? 当你后面的变量声明依赖之前的变量时，这样写代码时有帮助的。

    ```javascript
    // bad
    let i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // bad
    let i;
    const items = getItems();
    let dragonball;
    const goSportsTeam = true;
    let len;

    // good
    const goSportsTeam = true;
    const items = getItems();
    let dragonball;
    let i;
    let length;
    ```

  <a name="variables--define-where-used" /><a name="13.4"></a>
  - [13.4](#variables--define-where-used) 可以在任何地方给变量赋值,但是必须是合理的地方。

    > 为什么呢? `let` 和 `const` 是块级作用域，不是函数作用域。

    ```javascript
    // bad - unnecessary function call
    function checkName(hasName) {
      const name = getName();

      if (hasName === 'test') {
        return false;
      }

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }

    // good
    function checkName(hasName) {
      if (hasName === 'test') {
        return false;
      }

      const name = getName();

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }
    ```
  <a name="variables--no-chain-assignment" /><a name="13.5"></a>
  - [13.5](#variables--no-chain-assignment) 不要链式进行变量赋值。eslint: [`no-multi-assign`](https://eslint.org/docs/rules/no-multi-assign)

    > 为什么呢? 链式变量赋值创建隐式的全局变量。

    ```javascript
    // bad
    (function example() {
      // JavaScript interprets this as
      // let a = ( b = ( c = 1 ) );
      // The let keyword only applies to variable a; variables b and c become
      // global variables.
      let a = b = c = 1;
    }());

    console.log(a); // throws ReferenceError
    console.log(b); // 1
    console.log(c); // 1

    // good
    (function example() {
      let a = 1;
      let b = a;
      let c = a;
    }());

    console.log(a); // throws ReferenceError
    console.log(b); // throws ReferenceError
    console.log(c); // throws ReferenceError

    // the same applies for `const`
    ```

  <a name="variables--unary-increment-decrement" /><a name="13.6"></a>
  - [13.6](#variables--unary-increment-decrement) 避免使用一元加法（`++`）和减法（`--`）运算符。eslint [`no-plusplus`](https://eslint.org/docs/rules/no-plusplus)

    > 为什么呢? 按照eslint文档，一元加法和减法会自动插入分号会导致隐式的错误。同时使用`num +=1` 比 `num++` 或者`num ++` 更具表达性，更合理的语义。不允许一元加法和减法语句还避免你无意的预加或预减，这可能导致程序里出现未逾期的行为。

    ```javascript
    // bad

    const array = [1, 2, 3];
    let num = 1;
    num++;
    --num;

    let sum = 0;
    let truthyCount = 0;
    for (let i = 0; i < array.length; i++) {
      let value = array[i];
      sum += value;
      if (value) {
        truthyCount++;
      }
    }

    // good

    const array = [1, 2, 3];
    let num = 1;
    num += 1;
    num -= 1;

    const sum = array.reduce((a, b) => a + b, 0);
    const truthyCount = array.filter(Boolean).length;
    ```

<a name="variables--linebreak"></a>
  - [13.7](#variables--linebreak) 避免在赋值运算符`=`的前后断行。如果你违反了[`max-len`](https://eslint.org/docs/rules/max-len.html), 将值用括号括起来. eslint [`operator-linebreak`](https://eslint.org/docs/rules/operator-linebreak.html).

    > 为什么? 赋值运算符（`=`）前后换行可能混淆被赋的值。

    ```javascript
    // bad
    const foo =
      superLongLongLongLongLongLongLongLongFunctionName();

    // bad
    const foo
      = 'superLongLongLongLongLongLongLongLongString';

    // good
    const foo = (
      superLongLongLongLongLongLongLongLongFunctionName()
    );

    // good
    const foo = 'superLongLongLongLongLongLongLongLongString';
    ```

<a name="variables--no-unused-vars"></a>
  - [13.8](#variables--no-unused-vars) 不允许存在未使用的变量。eslint: [`no-unused-vars`](https://eslint.org/docs/rules/no-unused-vars)

    > 为什么呢? 代码中声明而未使用的变量最可能是不完全重构导致的错误。这类变量占据了代码空间会导致代码阅读者迷惑。

    ```javascript
    // bad

    var some_unused_var = 42;

    // Write-only variables are not considered as used.
    var y = 10;
    y = 5;

    // A read for a modification of itself is not considered as used.
    var z = 0;
    z = z + 1;

    // Unused function arguments.
    function getX(x, y) {
        return x;
    }

    // good

    function getXPlusY(x, y) {
      return x + y;
    }

    var x = 1;
    var y = a + 2;

    alert(getXPlusY(x, y));

    // 'type' is ignored even if unused because it has a rest property sibling.
    // This is a form of extracting an object that omits the specified keys.
    var { type, ...coords } = data;
    // 'coords' is now the 'data' object without its 'type' property.
    ```

**[⬆ 顶部](#内容索引)**

## 上升-Hoisting

  <a name="hoisting--about" /><a name="14.1"></a>
  - [14.1](#hoisting--about) `var`声明上升到他们最近的闭合函数作用域的顶部,不过它们的赋值不上升。 `const` 和 `let` 声明拥有一个新的概念叫做时间死区[Temporal Dead Zones (TDZ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_Dead_Zone). 这对于理解为什么typeof 不再安全很重要[typeof is no longer safe](http://es-discourse.com/t/why-typeof-is-no-longer-safe/15).

    ```javascript
    // we know this wouldn’t work (assuming there
    // is no notDefined global variable)
    function example() {
      console.log(notDefined); // => throws a ReferenceError
    }

    // creating a variable declaration after you
    // reference the variable will work due to
    // variable hoisting. Note: the assignment
    // value of `true` is not hoisted.
    function example() {
      console.log(declaredButNotAssigned); // => undefined
      var declaredButNotAssigned = true;
    }

    // the interpreter is hoisting the variable
    // declaration to the top of the scope,
    // which means our example could be rewritten as:
    function example() {
      let declaredButNotAssigned;
      console.log(declaredButNotAssigned); // => undefined
      declaredButNotAssigned = true;
    }

    // using const and let
    function example() {
      console.log(declaredButNotAssigned); // => throws a ReferenceError
      console.log(typeof declaredButNotAssigned); // => throws a ReferenceError
      const declaredButNotAssigned = true;
    }
    ```

  <a name="hoisting--anon-expressions" /><a name="14.2"></a>
  - [14.2](#hoisting--anon-expressions) 匿名函数表达式上升它们的变量名，而不上升函数赋值。

    ```javascript
    function example() {
      console.log(anonymous); // => undefined

      anonymous(); // => TypeError anonymous is not a function

      var anonymous = function () {
        console.log('anonymous function expression');
      };
    }
    ```

  <a name="hoisting--named-expresions" /><a name="hoisting--named-expressions" /><a name="14.3"></a>
  - [14.3](#hoisting--named-expressions) 命名的函数声明表达式上升变量名，不上升函数名和函数体。

    ```javascript
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      superPower(); // => ReferenceError superPower is not defined

      var named = function superPower() {
        console.log('Flying');
      };
    }

    // the same is true when the function name
    // is the same as the variable name.
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      var named = function named() {
        console.log('named');
      };
    }
    ```

  <a name="hoisting--declarations" /><a name="14.4"></a>
  - [14.4](#hoisting--declarations) 函数声明上升它们的名字和函数体。

    ```javascript
    function example() {
      superPower(); // => Flying

      function superPower() {
        console.log('Flying');
      }
    }
    ```

  - 更多信息参考[JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting/) by [Ben Cherry](http://www.adequatelygood.com/).

**[⬆ 顶部](#内容索引)**

## 比较表达式和等号-Comparison Operators & Equality

  <a name="comparison--eqeqeq" /><a name="15.1"></a>
  - [15.1](#comparison--eqeqeq) 使用全等/不全等 (`===`/`!==`) 运算符而不是 相等/不相等（`==` / `!=`）运算符。 eslint: [`eqeqeq`](https://eslint.org/docs/rules/eqeqeq.html)

  <a name="comparison--if" /><a name="15.2"></a>
  - [15.2](#comparison--if) 条件声明比如`if`声明对它们的表达式求值会通过`ToBoolean`抽象方法强制转换为布尔值，遵循下面的简单规则:

    - **Objects** 等价为 **true**
    - **Undefined** 等价为 **false**
    - **Null** 等价为 **false**
    - **Booleans** 等价为 **the value of the boolean**
    - **Numbers** 等价为 **false** 如果 **+0, -0, or NaN**, 否则 **true**
    - **Strings** 等价为 **false** 如果是空串 `''`, 否则 **true**

    ```javascript
    if ([0] && []) {
      // true
      // an array (even an empty one) is an object, objects will evaluate to true
    }
    ```

  <a name="comparison--shortcuts" /><a name="15.3"></a>
  - [15.3](#comparison--shortcuts) 布尔值使用简写, 但是比较字符串和数字时使用比较运算符。

    ```javascript
    // bad
    if (isValid === true) {
      // ...
    }

    // good
    if (isValid) {
      // ...
    }

    // bad
    if (name) {
      // ...
    }

    // good
    if (name !== '') {
      // ...
    }

    // bad
    if (collection.length) {
      // ...
    }

    // good
    if (collection.length > 0) {
      // ...
    }
    ```

  <a name="comparison--moreinfo" /><a name="15.4"></a>
  - [15.4](#comparison--moreinfo) 更多比较运算相关的信息，参考 [Truth Equality and JavaScript](https://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) by Angus Croll.

  <a name="comparison--switch-blocks" /><a name="15.5"></a>
  - [15.5](#comparison--switch-blocks) 使用花括号创建块当`case`和`default`条款中包含词法声明时。(e.g. `let`, `const`, `function`, and `class`). eslint: [`no-case-declarations`](https://eslint.org/docs/rules/no-case-declarations.html)

    > 为什么呢? 词法声明在整个`switch`块中是可见的，但初始化和赋值只在对应的`case`命中时发生。当多个`case`条目尝试定义相同的东西的时候会导致问题。

    ```javascript
    // bad
    switch (foo) {
      case 1:
        let x = 1;
        break;
      case 2:
        const y = 2;
        break;
      case 3:
        function f() {
          // ...
        }
        break;
      default:
        class C {}
    }

    // good
    switch (foo) {
      case 1: {
        let x = 1;
        break;
      }
      case 2: {
        const y = 2;
        break;
      }
      case 3: {
        function f() {
          // ...
        }
        break;
      }
      case 4:
        bar();
        break;
      default: {
        class C {}
      }
    }
    ```

  <a name="comparison--nested-ternaries" /><a name="15.6"></a>
  - [15.6](#comparison--nested-ternaries) 三元表达式不应该嵌套且最好是单行的。eslint: [`no-nested-ternary`](https://eslint.org/docs/rules/no-nested-ternary.html)

    ```javascript
    // bad
    const foo = maybe1 > maybe2
      ? "bar"
      : value1 > value2 ? "baz" : null;

    // split into 2 separated ternary expressions
    const maybeNull = value1 > value2 ? 'baz' : null;

    // better
    const foo = maybe1 > maybe2
      ? 'bar'
      : maybeNull;

    // best
    const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
    ```

  <a name="comparison--unneeded-ternary" /><a name="15.7"></a>
  - [15.7](#comparison--unneeded-ternary) 避免不需要的三元表达式。 eslint: [`no-unneeded-ternary`](https://eslint.org/docs/rules/no-unneeded-ternary.html)

    ```javascript
    // bad
    const foo = a ? a : b;
    const bar = c ? true : false;
    const baz = c ? false : true;

    // good
    const foo = a || b;
    const bar = !!c;
    const baz = !c;
    ```

  <a name="comparison--no-mixed-operators"></a>
  - [15.8](#comparison--no-mixed-operators) 当多个运算符混用, 使用括号裹起来.只有标准的算术运算符例外，因为它们的优先级是大多数人都明白的。 eslint: [`no-mixed-operators`](https://eslint.org/docs/rules/no-mixed-operators.html)

    > 为什么呢? 这提示了可读性同时澄清了开发者的意图。

    ```javascript
    // bad
    const foo = a && b < 0 || c > 0 || d + 1 === 0;

    // bad
    const bar = a ** b - 5 % d;

    // bad
    // one may be confused into thinking (a || b) && c
    if (a || b && c) {
      return d;
    }

    // good
    const foo = (a && b < 0) || c > 0 || (d + 1 === 0);

    // good
    const bar = (a ** b) - (5 % d);

    // good
    if (a || (b && c)) {
      return d;
    }

    // good
    const bar = a + b / c * d;
    ```

**[⬆ 顶部](#内容索引)**

## 块-Blocks

  <a name="blocks--braces" /><a name="16.1"></a>
  - [16.1](#blocks--braces) 所有的多行块使用花括号括起来。 eslint: [`nonblock-statement-body-position`](https://eslint.org/docs/rules/nonblock-statement-body-position)

    ```javascript
    // bad
    if (test)
      return false;

    // good
    if (test) return false;

    // good
    if (test) {
      return false;
    }

    // bad
    function foo() { return false; }

    // good
    function bar() {
      return false;
    }
    ```

  <a name="blocks--cuddled-elses" /><a name="16.2"></a>
  - [16.2](#blocks--cuddled-elses) 在`if`和`else`条件语句中的多行块时，将`else`和`if`块的闭合括号放在同一行。 eslint: [`brace-style`](https://eslint.org/docs/rules/brace-style.html)

    ```javascript
    // bad
    if (test) {
      thing1();
      thing2();
    }
    else {
      thing3();
    }

    // good
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```

  <a name="blocks--no-else-return" /><a name="16.3"></a>
  - [16.3](#blocks--no-else-return) 如果`if`块中执行了`return`语句，后续的`else`块就不是必须的了。若果`return`语句既在`if`块中，又在紧跟`if`块的`else if`块中,可与把它们拆分为多个`if`块。eslint: [`no-else-return`](https://eslint.org/docs/rules/no-else-return)

    ```javascript
    // bad
    function foo() {
      if (x) {
        return x;
      } else {
        return y;
      }
    }

    // bad
    function cats() {
      if (x) {
        return x;
      } else if (y) {
        return y;
      }
    }

    // bad
    function dogs() {
      if (x) {
        return x;
      } else {
        if (y) {
          return y;
        }
      }
    }

    // good
    function foo() {
      if (x) {
        return x;
      }

      return y;
    }

    // good
    function cats() {
      if (x) {
        return x;
      }

      if (y) {
        return y;
      }
    }

    // good
    function dogs(x) {
      if (x) {
        if (z) {
          return y;
        }
      } else {
        return z;
      }
    }
    ```

**[⬆ 顶部](#内容索引)**

## 控制语句-Control Statements

  <a name="control-statements"></a>
  - [17.1](#control-statements) 假如你的控制语句(`if`, `while` etc.)太长或者超过最大行宽,每个/组条件可以单独占一行。逻辑运算符要在起始位置。

    > 为什么呢? 需要运算符在行头对齐是为了了和函数的链式调用保持一致。这同样也提高了可读性，使得视觉上易于区分复杂的逻辑。

    ```javascript
    // bad
    if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
      thing1();
    }

    // bad
    if (foo === 123 &&
      bar === 'abc') {
      thing1();
    }

    // bad
    if (foo === 123
      && bar === 'abc') {
      thing1();
    }

    // bad
    if (
      foo === 123 &&
      bar === 'abc'
    ) {
      thing1();
    }

    // good
    if (
      foo === 123
      && bar === 'abc'
    ) {
      thing1();
    }

    // good
    if (
      (foo === 123 || bar === 'abc')
      && doesItLookGoodWhenItBecomesThatLong()
      && isThisReallyHappening()
    ) {
      thing1();
    }

    // good
    if (foo === 123 && bar === 'abc') {
      thing1();
    }
    ```

  <a name="control-statement--value-selection" /><a name="control-statements--value-selection"></a>
  - [17.2](#control-statements--value-selection) 在控制语句中别使用选择运算符。这和之前的选择运算符控制变量赋值要区分来看。

    ```javascript
    // bad
    !isRunning && startRunning();

    // good
    if (!isRunning) {
      startRunning();
    }
    ```

**[⬆ 顶部](#内容索引)**

## 注释-Comments

  <a name="comments--multiline" /><a name="17.1"></a>
  - [18.1](#comments--multiline) 使用 `/** ... */` 来多行注释。

    ```javascript
    // bad
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param {String} tag
    // @return {Element} element
    function make(tag) {

      // ...

      return element;
    }

    // good
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }
    ```

  <a name="comments--singleline" /><a name="17.2"></a>
  - [18.2](#comments--singleline) 使用 `//` 来单行注释。 将单行注释置于要说明的代码的上方。注释之前要有一个空行，除非是在块的第一行。

    ```javascript
    // bad
    const active = true;  // is current tab

    // good
    // is current tab
    const active = true;

    // bad
    function getType() {
      console.log('fetching type...');
      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }

    // good
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }

    // also good
    function getType() {
      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }
    ```

  <a name="comments--spaces"></a>
  - [18.3](#comments--spaces) 使用一个空格做为注释的起始易于阅读。eslint: [`spaced-comment`](https://eslint.org/docs/rules/spaced-comment)

    ```javascript
    // bad
    //is current tab
    const active = true;

    // good
    // is current tab
    const active = true;

    // bad
    /**
     *make() returns a new element
     *based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }

    // good
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }
    ```

  <a name="comments--actionitems" /><a name="17.3"></a>
  - [18.4](#comments--actionitems) 给注释加上`FIXME`或`TODO`协助其他开发者快速理解，如果你指出一个问题需要重现或者你建议一个解决问题的方案需要实现。不同于规则的注释，他们是可操作的。操作是：`FIXME: -- 需要想出方案`或`TODO: -- 需要实现`。一般都是看到了隐患时的注释。

  <a name="comments--fixme" /><a name="17.4"></a>
  - [18.5](#comments--fixme) 使用 `// FIXME:` 来注释问题.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // FIXME: shouldn’t use a global here
        total = 0;
      }
    }
    ```

  <a name="comments--todo" /><a name="17.5"></a>
  - [18.6](#comments--todo) 使用 `// TODO:` 解决问题的方案。

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // TODO: total should be configurable by an options param
        this.total = 0;
      }
    }
    ```

**[⬆ 顶部](#内容索引)**

## 空格-Whitespace

  <a name="whitespace--spaces" /><a name="18.1"></a>
  - [19.1](#whitespace--spaces) 使用软tabs (空格字符) 2个空格来缩进. eslint: [`indent`](https://eslint.org/docs/rules/indent.html)

    ```javascript
    // bad
    function foo() {
    ∙∙∙∙let name;
    }

    // bad
    function bar() {
    ∙let name;
    }

    // good
    function baz() {
    ∙∙let name;
    }
    ```

  <a name="whitespace--before-blocks" /><a name="18.2"></a>
  - [19.2](#whitespace--before-blocks) 在左大括号前需要一个空格。 eslint: [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks.html)

    ```javascript
    // bad
    function test(){
      console.log('test');
    }

    // good
    function test() {
      console.log('test');
    }

    // bad
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });

    // good
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    ```

  <a name="whitespace--around-keywords" /><a name="18.3"></a>
  - [19.3](#whitespace--around-keywords) 在控制语句(`if`, `while` 等。)的左开括号前添加一个空格. 函数调用和声明时参数列表和行数名之间不能有空格。 eslint: [`keyword-spacing`](https://eslint.org/docs/rules/keyword-spacing.html)

    ```javascript
    // bad
    if(isJedi) {
      fight ();
    }

    // good
    if (isJedi) {
      fight();
    }

    // bad
    function fight () {
      console.log ('Swooosh!');
    }

    // good
    function fight() {
      console.log('Swooosh!');
    }
    ```

  <a name="whitespace--infix-ops" /><a name="18.4"></a>
  - [19.4](#whitespace--infix-ops) 操作符使用空格隔开。 eslint: [`space-infix-ops`](https://eslint.org/docs/rules/space-infix-ops.html)

    ```javascript
    // bad
    const x=y+5;

    // good
    const x = y + 5;
    ```

  <a name="whitespace--newline-at-end" /><a name="18.5"></a>
  - [19.5](#whitespace--newline-at-end) 文件使用单独的换行符结尾。eslint: [`eol-last`](https://github.com/eslint/eslint/blob/master/docs/rules/eol-last.md)

    ```javascript
    // bad
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;
    ```

    ```javascript
    // bad
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;↵
    ↵
    ```

    ```javascript
    // good
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;↵
    ```

  <a name="whitespace--chains" /><a name="18.6"></a>
  - [19.6](#whitespace--chains) 长的函数链式调用(两个以上)使用缩进排版。点运算符要在行首， 用来强调这行是一个行数调用，不是一个新语句。 eslint: [`newline-per-chained-call`](https://eslint.org/docs/rules/newline-per-chained-call) [`no-whitespace-before-property`](https://eslint.org/docs/rules/no-whitespace-before-property)

    ```javascript
    // bad
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // bad
    $('#items').
      find('.selected').
        highlight().
        end().
      find('.open').
        updateCount();

    // good
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();

    // bad
    const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
        .attr('width', (radius + margin) * 2).append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    // good
    const leds = stage.selectAll('.led')
        .data(data)
      .enter().append('svg:svg')
        .classed('led', true)
        .attr('width', (radius + margin) * 2)
      .append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    // good
    const leds = stage.selectAll('.led').data(data);
    ```

  <a name="whitespace--after-blocks" /><a name="18.7"></a>
  - [19.7](#whitespace--after-blocks) 在代码块和下一条语句间预留一个空白行。

    ```javascript
    // bad
    if (foo) {
      return bar;
    }
    return baz;

    // good
    if (foo) {
      return bar;
    }

    return baz;

    // bad
    const obj = {
      foo() {
      },
      bar() {
      },
    };
    return obj;

    // good
    const obj = {
      foo() {
      },

      bar() {
      },
    };

    return obj;

    // bad
    const arr = [
      function foo() {
      },
      function bar() {
      },
    ];
    return arr;

    // good
    const arr = [
      function foo() {
      },

      function bar() {
      },
    ];

    return arr;
    ```

  <a name="whitespace--padded-blocks" /><a name="18.8"></a>
  - [19.8](#whitespace--padded-blocks) 不要在代码块中无意义的添加空白行。 eslint: [`padded-blocks`](https://eslint.org/docs/rules/padded-blocks.html)

    ```javascript
    // bad
    function bar() {

      console.log(foo);

    }

    // bad
    if (baz) {

      console.log(qux);
    } else {
      console.log(foo);

    }

    // bad
    class Foo {

      constructor(bar) {
        this.bar = bar;
      }
    }

    // good
    function bar() {
      console.log(foo);
    }

    // good
    if (baz) {
      console.log(qux);
    } else {
      console.log(foo);
    }
    ```

  <a name="whitespace--in-parens" /><a name="18.9"></a>
  - [19.9](#whitespace--in-parens) 不要在圆括号内部添加空格。 eslint: [`space-in-parens`](https://eslint.org/docs/rules/space-in-parens.html)

    ```javascript
    // bad
    function bar( foo ) {
      return foo;
    }

    // good
    function bar(foo) {
      return foo;
    }

    // bad
    if ( foo ) {
      console.log(foo);
    }

    // good
    if (foo) {
      console.log(foo);
    }
    ```

  <a name="whitespace--in-brackets" /><a name="18.10"></a>
  - [19.10](#whitespace--in-brackets) 数组中括号的首尾不允许有空格。eslint: [`array-bracket-spacing`](https://eslint.org/docs/rules/array-bracket-spacing.html)

    ```javascript
    // bad
    const foo = [ 1, 2, 3 ];
    console.log(foo[ 0 ]);

    // good
    const foo = [1, 2, 3];
    console.log(foo[0]);
    ```

  <a name="whitespace--in-braces" /><a name="18.11"></a>
  - [19.11](#whitespace--in-braces) 花括号的首尾需要插入一个空格。 eslint: [`object-curly-spacing`](https://eslint.org/docs/rules/object-curly-spacing.html)

    ```javascript
    // bad
    const foo = {clark: 'kent'};

    // good
    const foo = { clark: 'kent' };
    ```

  <a name="whitespace--max-len" /><a name="18.12"></a>
  - [19.12](#whitespace--max-len) 避免一行代码超过100字符(包括空白)。 注意: 按照 [之前的规范](#strings--line-length), 长字符串时免于这条规则的，不应该被断行。 eslint: [`max-len`](https://eslint.org/docs/rules/max-len.html)

    > 为什么呢? 这确保可读性和可维护性(读的懂才知道怎么改，哪里该改，而不是一刀下去问题压制了，引入了更多的bug)。

    ```javascript
    // bad
    const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

    // bad
    $.ajax({ method: 'POST', url: 'https://airbnb.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

    // good
    const foo = jsonData
      && jsonData.foo
      && jsonData.foo.bar
      && jsonData.foo.bar.baz
      && jsonData.foo.bar.baz.quux
      && jsonData.foo.bar.baz.quux.xyzzy;

    // good
    $.ajax({
      method: 'POST',
      url: 'https://airbnb.com/',
      data: { name: 'John' },
    })
      .done(() => console.log('Congratulations!'))
      .fail(() => console.log('You have failed this city.'));
    ```

  <a name="whitespace--block-spacing"></a>
  - [19.13](#whitespace--block-spacing) 代码块如果在一行，左右花括号与语句间需要有空格隔开。这规则同样对控制语句器作用。 eslint: [`block-spacing`](https://eslint.org/docs/rules/block-spacing)

    ```javascript
    // bad
    function foo() {return true;}
    if (foo) { bar = 0;}

    // good
    function foo() { return true; }
    if (foo) { bar = 0; }
    ```

  <a name="whitespace--comma-spacing"></a>
  - [19.14](#whitespace--comma-spacing) 避免逗号前有空格，逗号后面需要一个空格。eslint: [`comma-spacing`](https://eslint.org/docs/rules/comma-spacing)

    ```javascript
    // bad
    var foo = 1,bar = 2;
    var arr = [1 , 2];

    // good
    var foo = 1, bar = 2;
    var arr = [1, 2];
    ```

  <a name="whitespace--computed-property-spacing"></a>
  - [19.15](#whitespace--computed-property-spacing) 计算属性括号中强制插入空格。 eslint: [`computed-property-spacing`](https://eslint.org/docs/rules/computed-property-spacing)

    ```javascript
    // bad
    obj[foo ]
    obj[ 'foo']
    var x = {[ b ]: a}
    obj[foo[ bar ]]

    // good
    obj[foo]
    obj['foo']
    var x = { [b]: a }
    obj[foo[bar]]
    ```

  <a name="whitespace--func-call-spacing"></a>
  - [19.16](#whitespace--func-call-spacing) 避免函数和它们的调用之间有空白。 eslint: [`func-call-spacing`](https://eslint.org/docs/rules/func-call-spacing)

    ```javascript
    // bad
    func ();

    func
    ();

    // good
    func();
    ```

  <a name="whitespace--key-spacing"></a>
  - [19.17](#whitespace--key-spacing) 对象直面量属性的键值之间用空格风格。 eslint: [`key-spacing`](https://eslint.org/docs/rules/key-spacing)

    ```javascript
    // bad
    var obj = { "foo" : 42 };
    var obj2 = { "foo":42 };

    // good
    var obj = { "foo": 42 };
    ```

  <a name="whitespace--no-trailing-spaces"></a>
  - [19.18](#whitespace--no-trailing-spaces) 避免在行尾留有空格。 eslint: [`no-trailing-spaces`](https://eslint.org/docs/rules/no-trailing-spaces)

  <a name="whitespace--no-multiple-empty-lines"></a>
  - [19.19](#whitespace--no-multiple-empty-lines) 避免多行空行，只允许文件结尾有一行空行。eslint: [`no-multiple-empty-lines`](https://eslint.org/docs/rules/no-multiple-empty-lines)

    <!-- markdownlint-disable MD012 -->
    ```javascript
    // bad
    var x = 1;



    var y = 2;

    // good
    var x = 1;

    var y = 2;
    ```
    <!-- markdownlint-enable MD012 -->

**[⬆ 顶部](#内容索引)**

## 逗号-Commas

  <a name="commas--leading-trailing" /><a name="19.1"></a>
  - [20.1](#commas--leading-trailing) 逗号不允许在行首。 eslint: [`comma-style`](https://eslint.org/docs/rules/comma-style.html)

    ```javascript
    // bad
    const story = [
        once
      , upon
      , aTime
    ];

    // good
    const story = [
      once,
      upon,
      aTime,
    ];

    // bad
    const hero = {
        firstName: 'Ada'
      , lastName: 'Lovelace'
      , birthYear: 1815
      , superPower: 'computers'
    };

    // good
    const hero = {
      firstName: 'Ada',
      lastName: 'Lovelace',
      birthYear: 1815,
      superPower: 'computers',
    };
    ```

  <a name="commas--dangling" /><a name="19.2"></a>
  - [20.2](#commas--dangling) 附加尾部逗号. eslint: [`comma-dangle`](https://eslint.org/docs/rules/comma-dangle.html)

    > 为什么呢? 这可以使得git diff 时更简洁. 同时编译器比如`babel`会去除附加的逗号，这意味着你不用担心非现代浏览器中[尾部附加逗号的问题](https://github.com/airbnb/javascript/blob/es5-deprecated/es5/README.md#commas).

    ```diff
    // bad - git diff without trailing comma
    const hero = {
         firstName: 'Florence',
    -    lastName: 'Nightingale'
    +    lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing']
    };

    // good - git diff with trailing comma
    const hero = {
         firstName: 'Florence',
         lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing'],
    };
    ```

    ```javascript
    // bad
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully'
    };

    const heroes = [
      'Batman',
      'Superman'
    ];

    // good
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully',
    };

    const heroes = [
      'Batman',
      'Superman',
    ];

    // bad
    function createHero(
      firstName,
      lastName,
      inventorOf
    ) {
      // does nothing
    }

    // good
    function createHero(
      firstName,
      lastName,
      inventorOf,
    ) {
      // does nothing
    }

    // good (note that a comma must not appear after a "rest" element)
    function createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    ) {
      // does nothing
    }

    // bad
    createHero(
      firstName,
      lastName,
      inventorOf
    );

    // good
    createHero(
      firstName,
      lastName,
      inventorOf,
    );

    // good (note that a comma must not appear after a "rest" element)
    createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    );
    ```

**[⬆ 顶部](#内容索引)**

## 分号-Semicolons

  <a name="semicolons--required" /><a name="20.1"></a>
  - [21.1](#semicolons--required) **Yup.** eslint: [`semi`](https://eslint.org/docs/rules/semi.html)

    > 为什么呢? 当JavaScript遭遇到没有分号的换行，它按一套规则[Automatic Semicolon Insertion](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion) 来决定是否应该认定换行是语句的结尾,顾名思义JS将按规则补全分号到代码中去，如果它认为有必要. ASI 包含该了一些古怪的行为,因此如果JavaScript曲解了你的换行你的代码会奔溃。这些规则随着更多的特性加入到JavaScript 将越来越复杂。 显式的中断你的语句和配置你的语法校验器去捕获分号缺失将有助于避免问题。

    ```javascript
    // bad - raises exception
    const luke = {}
    const leia = {}
    [luke, leia].forEach(jedi => jedi.father = 'vader')

    // bad - raises exception
    const reaction = "No! That’s impossible!"
    (async function meanwhileOnTheFalcon() {
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }())

    // bad - returns `undefined` instead of the value on the next line - always happens when `return` is on a line by itself because of ASI!
    function foo() {
      return
        'search your feelings, you know it to be foo'
    }

    // good
    const luke = {};
    const leia = {};
    [luke, leia].forEach((jedi) => {
      jedi.father = 'vader';
    });

    // good
    const reaction = "No! That’s impossible!";
    (async function meanwhileOnTheFalcon() {
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }());

    // good
    function foo() {
      return 'search your feelings, you know it to be foo';
    }
    ```

    [更多参考](https://stackoverflow.com/questions/7365172/semicolon-before-self-invoking-function/7365214#7365214).

**[⬆ 顶部](#内容索引)**

## 强制类型转换-Type Casting & Coercion

  <a name="coercion--explicit" /><a name="21.1"></a>
  - [22.1](#coercion--explicit) 在语句的开始处执行强制类型转换。Perform type coercion at the beginning of the statement.

  <a name="coercion--strings" /><a name="21.2"></a>
  - [22.2](#coercion--strings)  Strings:字符串转换不使用`new`关键字 eslint: [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    ```javascript
    // => this.reviewScore = 9;

    // bad
    const totalScore = new String(this.reviewScore); // typeof totalScore is "object" not "string"

    // bad
    const totalScore = this.reviewScore + ''; // invokes this.reviewScore.valueOf()

    // bad
    const totalScore = this.reviewScore.toString(); // isn’t guaranteed to return a string

    // good
    const totalScore = String(this.reviewScore);
    ```

  <a name="coercion--numbers"></a><a name="21.3"></a>
  - [22.3](#coercion--numbers) 强制转换数字: 使用 `Number` 关键字做类型转换或者 `parseInt`需要明确设置转换进制。eslint: [`radix`](https://eslint.org/docs/rules/radix) [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    ```javascript
    const inputValue = '4';

    // bad
    const val = new Number(inputValue);

    // bad
    const val = +inputValue;

    // bad
    const val = inputValue >> 0;

    // bad
    const val = parseInt(inputValue);

    // good
    const val = Number(inputValue);

    // good
    const val = parseInt(inputValue, 10);
    ```

  <a name="coercion--comment-deviations" /><a name="21.4"></a>
  - [22.4](#coercion--comment-deviations) 如果你做的东西`parseInt`是你的瓶颈,需要位移来类型转换[performance reasons](https://jsperf.com/coercion-vs-casting/3), 留下注释解释下为什么以及你在做什么。

    ```javascript
    // good
    /**
     * parseInt was the reason my code was slow.
     * Bitshifting the String to coerce it to a
     * Number made it a lot faster.
     */
    const val = inputValue >> 0;
    ```

  <a name="coercion--bitwise" /><a name="21.5"></a>
  - [22.5](#coercion--bitwise) **注意:** 使用位移操作符时要小心一些情况。 数字在JavaScript中是64位表示 [64-bit values](https://es5.github.io/#x4.3.19), 但位移操作符总是放回32为整型([source](https://es5.github.io/#x11.7)). 当整数值大于32位时位于运算会导致意外的行为。 [Discussion](https://github.com/airbnb/javascript/issues/109). 最大的无符号32位整数是 2,147,483,647:

    ```javascript
    2147483647 >> 0; // => 2147483647
    2147483648 >> 0; // => -2147483648
    2147483649 >> 0; // => -2147483647
    ```

  <a name="coercion--booleans" /><a name="21.6"></a>
  - [22.6](#coercion--booleans) 布尔值: eslint: [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    ```javascript
    const age = 0;

    // bad
    const hasAge = new Boolean(age);

    // good
    const hasAge = Boolean(age);

    // best
    const hasAge = !!age;
    ```

**[⬆ 顶部](#内容索引)**

## 命名规则-Naming Conventions

  <a name="naming--descriptive" /><a name="22.1"></a>
  - [23.1](#naming--descriptive) 避免单字母名称。 命名需要语义化。eslint: [`id-length`](https://eslint.org/docs/rules/id-length)

    ```javascript
    // bad
    function q() {
      // ...
    }

    // good
    function query() {
      // ...
    }
    ```

  <a name="naming--camelCase" /><a name="22.2"></a>
  - [23.2](#naming--camelCase) 使用驼峰命名法（camelCase）命名objects，functions, and instances. eslint: [`camelcase`](https://eslint.org/docs/rules/camelcase.html)

    ```javascript
    // bad
    const OBJEcttsssss = {};
    const this_is_my_object = {};
    function c() {}

    // good
    const thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

  <a name="naming--PascalCase" /><a name="22.3"></a>
  - [23.3](#naming--PascalCase) 当且仅当命名构造函数或类名时使用帕斯卡命名法 (PascalCase)。 eslint: [`new-cap`](https://eslint.org/docs/rules/new-cap.html)

    ```javascript
    // bad
    function user(options) {
      this.name = options.name;
    }

    const bad = new user({
      name: 'nope',
    });

    // good
    class User {
      constructor(options) {
        this.name = options.name;
      }
    }

    const good = new User({
      name: 'yup',
    });
    ```

  <a name="naming--leading-underscore" /><a name="22.4"></a>
  - [23.4](#naming--leading-underscore) 不要在名字首尾用下划线。 eslint: [`no-underscore-dangle`](https://eslint.org/docs/rules/no-underscore-dangle.html)

    > 为什么呢? JavaScript 没有私有属性和私有方法的概念。 尽管首部下划线是通用约定的代表“private”，实际上这些属性仍然公开的，和那部分约定公开的APi一样。这个习惯可能会导致开发者误认为修改私有属性不算是破坏，或者测试时不需要考虑。如果你想私有变量或函数，它不应该显式的出现。

    ```javascript
    // bad
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';
    this._firstName = 'Panda';

    // good
    this.firstName = 'Panda';

    // good, in environments where WeakMaps are available
    // see https://kangax.github.io/compat-table/es6/#test-WeakMap
    const firstNames = new WeakMap();
    firstNames.set(this, 'Panda');
    ```

  <a name="naming--self-this"></a><a name="22.5"></a>
  - [23.5](#naming--self-this) 不要用参数指向`this`。使用箭头函数或者 [Function#bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind).

    ```javascript
    // bad
    function foo() {
      const self = this;
      return function () {
        console.log(self);
      };
    }

    // bad
    function foo() {
      const that = this;
      return function () {
        console.log(that);
      };
    }

    // good
    function foo() {
      return () => {
        console.log(this);
      };
    }
    ```

  <a name="naming--filename-matches-export" /><a name="22.6"></a>
  - [23.6](#naming--filename-matches-export) 基本文件名应该和它的默认输出(default export)保持完全一致。

    ```javascript
    // file 1 contents
    class CheckBox {
      // ...
    }
    export default CheckBox;

    // file 2 contents
    export default function fortyTwo() { return 42; }

    // file 3 contents
    export default function insideDirectory() {}

    // in some other file
    // bad
    import CheckBox from './checkBox'; // PascalCase import/export, camelCase filename
    import FortyTwo from './FortyTwo'; // PascalCase import/filename, camelCase export
    import InsideDirectory from './InsideDirectory'; // PascalCase import/filename, camelCase export

    // bad
    import CheckBox from './check_box'; // PascalCase import/export, snake_case filename
    import forty_two from './forty_two'; // snake_case import/filename, camelCase export
    import inside_directory from './inside_directory'; // snake_case import, camelCase export
    import index from './inside_directory/index'; // requiring the index file explicitly
    import insideDirectory from './insideDirectory/index'; // requiring the index file explicitly

    // good
    import CheckBox from './CheckBox'; // PascalCase export/import/filename
    import fortyTwo from './fortyTwo'; // camelCase export/import/filename
    import insideDirectory from './insideDirectory'; // camelCase export/import/directory name/implicit "index"
    // ^ supports both insideDirectory.js and insideDirectory/index.js
    ```

  <a name="naming--camelCase-default-export" /><a name="22.7"></a>
  - [23.7](#naming--camelCase-default-export) 使用驼峰命名方式（camelCase）当默认输出的是函数时。 文件名应该和函数名一致。

    ```javascript
    function makeStyleGuide() {
      // ...
    }

    export default makeStyleGuide;
    ```

  <a name="naming--PascalCase-singleton" /><a name="22.8"></a>
  - [23.8](#naming--PascalCase-singleton) 使用帕斯卡(PascalCase) 命名法 当输出(export)的是构造器(constructor) / 类(class) / 单例(singleton) / 函数库(function library) / 暴露到的对象(bare object)。

    ```javascript
    const AirbnbStyleGuide = {
      es6: {
      },
    };

    export default AirbnbStyleGuide;
    ```

  <a name="naming--Acronyms-and-Initialisms"></a>
  - [23.9](#naming--Acronyms-and-Initialisms) 英文缩写要么全部大写，要么全部小写。

    > Why? Names are for readability, not to appease a computer algorithm.

    ```javascript
    // bad
    import SmsContainer from './containers/SmsContainer';

    // bad
    const HttpRequests = [
      // ...
    ];

    // good
    import SMSContainer from './containers/SMSContainer';

    // good
    const HTTPRequests = [
      // ...
    ];

    // also good
    const httpRequests = [
      // ...
    ];

    // best
    import TextMessageContainer from './containers/TextMessageContainer';

    // best
    const requests = [
      // ...
    ];
    ``` 
 
  <a name="naming--uppercase"></a>
  - [23.10](#naming--uppercase) 只有在变量是暴露的，是一个常量`const`（不能重新赋值），编程人员相信它（以及它嵌套的属性）不会改变，你需要大写变量名声明为常量。

    > 为什么呢? 这是一个额外的工具(大写常量名)用来协助程序员在确定一个变量是否会改变。大写的变量(UPPERCASE_VARIABLES)是让程序员知道他们可以信任这个变量(以及它们的属性)不会改变。
    - 常量化所有变量如何？ - 这不是必须的, 因此大写so uppercasing should not be used for constants within a file. It should be used for exported constants however.
    - What about exported objects? - Uppercase at the top level of export  (e.g. `EXPORTED_OBJECT.key`) and maintain that all nested properties do not change.

    ```javascript
    // bad
    const PRIVATE_VARIABLE = 'should not be unnecessarily uppercased within a file';

    // bad
    export const THING_TO_BE_CHANGED = 'should obviously not be uppercased';

    // bad
    export let REASSIGNABLE_VARIABLE = 'do not use let with uppercase variables';

    // ---

    // allowed but does not supply semantic value
    export const apiKey = 'SOMEKEY';

    // better in most cases
    export const API_KEY = 'SOMEKEY';

    // ---

    // bad - unnecessarily uppercases key while adding no semantic value
    export const MAPPING = {
      KEY: 'value'
    };

    // good
    export const MAPPING = {
      key: 'value'
    };
    ```

**[⬆ 顶部](#内容索引)**

## 访问器-Accessors

  <a name="accessors--not-required" /><a name="23.1"></a>
  - [24.1](#accessors--not-required) 属性不需要访问函数。

  <a name="accessors--no-getters-setters" /><a name="23.2"></a>
  - [24.2](#accessors--no-getters-setters) 不要使用JavaScript getters/setters 因为他们造成预想不到的副作用同时难以测试,维护,预测。 相反你可以构造访问器例如：`getVal()` 和 `setVal('hello')`。

    ```javascript
    // bad
    class Dragon {
      get age() {
        // ...
      }

      set age(value) {
        // ...
      }
    }

    // good
    class Dragon {
      getAge() {
        // ...
      }

      setAge(value) {
        // ...
      }
    }
    ```

  <a name="accessors--boolean-prefix" /><a name="23.3"></a>
  - [24.3](#accessors--boolean-prefix) 如果属性/方法布尔值（`boolean`）使用 `isVal()` 和 `hasVal()`。

    ```javascript
    // bad
    if (!dragon.age()) {
      return false;
    }

    // good
    if (!dragon.hasAge()) {
      return false;
    }
    ```

  <a name="accessors--consistent" /><a name="23.4"></a>
  - [24.4](#accessors--consistent) 可以创建 `get()` 和 `set()` 函数, 但必须是一致的.

    ```javascript
    class Jedi {
      constructor(options = {}) {
        const lightsaber = options.lightsaber || 'blue';
        this.set('lightsaber', lightsaber);
      }

      set(key, val) {
        this[key] = val;
      }

      get(key) {
        return this[key];
      }
    }
    ```

**[⬆ 顶部](#内容索引)**

## 事件-Events

  <a name="events--hash" /><a name="24.1"></a>
  - [25.1](#events--hash) 当需要携带数据载荷（data payloads) 给触发的视觉是（不管是DOM事件还是其它属性事件比如vue自定义事件），传递一个对象字面量(也称为"hash") 代替具体的值. 这允许后续的贡献者添加更多数据到事件载荷，而不用查找和更新每一个使用了这个事件的处理器. 比如:

    ```javascript
    // bad
    $(this).trigger('listingUpdated', listing.id);

    // ...

    $(this).on('listingUpdated', (e, listingID) => {
      // do something with listingID
    });
    ```

    prefer:

    ```javascript
    // good
    $(this).trigger('listingUpdated', { listingID: listing.id });

    // ...

    $(this).on('listingUpdated', (e, data) => {
      // do something with data.listingID
    });
    ```

  **[⬆ 顶部](#内容索引)**

## jQuery

  <a name="jquery--dollar-prefix" /><a name="25.1"></a>
  - [26.1](#jquery--dollar-prefix) jQuery对象变量加前缀`$`。

    ```javascript
    // bad
    const sidebar = $('.sidebar');

    // good
    const $sidebar = $('.sidebar');

    // good
    const $sidebarBtn = $('.sidebar-btn');
    ```

  <a name="jquery--cache" /><a name="25.2"></a>
  - [26.2](#jquery--cache) 缓存JQuery查找结果(思路是减少性能损耗大的操作)。

    ```javascript
    // bad
    function setSidebar() {
      $('.sidebar').hide();

      // ...

      $('.sidebar').css({
        'background-color': 'pink',
      });
    }

    // good
    function setSidebar() {
      const $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...

      $sidebar.css({
        'background-color': 'pink',
      });
    }
    ```

  <a name="jquery--queries" /><a name="25.3"></a>
  - [26.3](#jquery--queries) For DOM queries use Cascading `$('.sidebar ul')` or parent > child `$('.sidebar > ul')`. [jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)

  <a name="jquery--find" /><a name="25.4"></a>
  - [26.4](#jquery--find) Use `find` with scoped jQuery object queries.

    ```javascript
    // bad
    $('ul', '.sidebar').hide();

    // bad
    $('.sidebar').find('ul').hide();

    // good
    $('.sidebar ul').hide();

    // good
    $('.sidebar > ul').hide();

    // good
    $sidebar.find('ul').hide();
    ```

**[⬆ 顶部](#内容索引)**

## es5兼容-ECMAScript 5 Compatibility

  <a name="es5-compat--kangax" /><a name="26.1"></a>
  - [27.1](#es5-compat--kangax) 参考 [Kangax](https://twitter.com/kangax/)’s ES5 [compatibility table](https://kangax.github.io/es5-compat-table/).

**[⬆ 顶部](#内容索引)**

<a name="ecmascript-6-styles"></a>
## es6+风格-ECMAScript 6+ (ES 2015+) Styles

  <a name="es6-styles" /><a name="27.1"></a>
  - [28.1](#es6-styles) 下面是各种ES6+特性的链接的集合。

1. [箭头函数-Arrow Functions](#箭头函数-arrow-functions)
1. [类和构造器-Classes & Constructors](#类和构造器-classes--constructors)
1. [对象简写-Object Shorthand](#es6-object-shorthand)
1. [对象简洁-Object Concise](#es6-object-concise)
1. [对象计算属性-Object Computed Properties](#es6-computed-properties)
1. [字符串模板-Template Strings](#es6-template-literals)
1. [解构-Destructuring](#解构-destructuring)
1. [默认参数-Default Parameters](#es6-default-parameters)
1. [剩余运算符-Rest](#es6-rest)
1. [数组展开-Array Spreads](#es6-array-spreads)
1. [变量声明-Let and Const](#references)
1. [幂运算操作符-Exponentiation Operator](#es2016-properties--exponentiation-operator)
1. [迭代器和生成器-Iterators and Generators](#迭代器和生成器-iterators-and-generators)
1. [模块-Modules](#模块-modules)

  <a name="tc39-proposals"></a>
  - [28.2](#tc39-proposals) 不要使用 [TC39 提案](https://github.com/tc39/proposals) 它还没到点第三阶段.

    > 为什么呢? [这不是最终的方案](https://tc39.github.io/process-document/), 它的议题会改变或者完整的撤回。 我们要用JavaScript, 但是提案还不是。

**[⬆ 顶部](#内容索引)**

## 标准库-Standard Library

  [标准库](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects)
  中包含一些功能破坏但由于遗留原因而保留的程序。

  <a name="standard-library--isnan"></a>
  - [29.1](#standard-library--isnan) 用 `Number.isNaN` 代替 `isNaN`。
    eslint: [`no-restricted-globals`](https://eslint.org/docs/rules/no-restricted-globals)

    > 为什么呢? 全局`isNaN`强制非数字类型(non-numbers)转为数字类型（numbers)，其中任何强制转化为NaN的都返回真。
    > 如果想要这个行为，明确的表示出来。

    ```javascript
    // bad
    isNaN('1.2'); // false
    isNaN('1.2.3'); // true

    // good
    Number.isNaN('1.2.3'); // false
    Number.isNaN(Number('1.2.3')); // true
    ```

  <a name="standard-library--isfinite"></a>
  - [29.2](#standard-library--isfinite) 使用`Number.isFinite`代替全局`isFinite`.
    eslint: [`no-restricted-globals`](https://eslint.org/docs/rules/no-restricted-globals)

    > 为什么呢? 全局`isFinite`强制转换非数字类型（non-numbers）为数字类型, 其中可以强转为无限大的返回真。
    > 如果想要这个行为，明确的表示出来。

    ```javascript
    // bad
    isFinite('2e3'); // true

    // good
    Number.isFinite('2e3'); // false
    Number.isFinite(parseInt('2e3', 10)); // true
    ```

**[⬆ 顶部](#内容索引)**

## 测试-Testing

  <a name="testing--yup" /><a name="28.1"></a>
  - [30.1](#testing--yup) **这是极好的。**

    ```javascript
    function foo() {
      return true;
    }
    ```

  <a name="testing--for-real" /><a name="28.2"></a>
  - [30.2](#testing--for-real) **No, but seriously**:
    - 任何一个测试框架都需要写测试用例!
    - 尽可能写多的小纯函数， 同时最小化突变发生的位置(单一职责?)。
    - 小心打桩(stubs)和模拟(mocks) - 它们使得你们的测试脆弱。
    - 我们主要使用[`mocha`](https://www.npmjs.com/package/mocha)和[`jest`](https://www.npmjs.com/package/jest) 在 Airbnb. [`tape`](https://www.npmjs.com/package/tape) 有时也被用来测试小的独立的模块.
    - 100% 测试覆盖率是一个好目标要尽力达成，即使实际中并不总是能够达成。
    - 任何候你修复了一个bug， _写一个回归测试_. 修复的bug没有回归测试将来几乎肯定再次出现。

**[⬆ 顶部](#内容索引)**

## 性能-Performance

  - [On Layout & Web Performance](https://www.kellegous.com/j/2013/01/26/layout-performance/)
  - [String vs Array Concat](https://jsperf.com/string-vs-array-concat/2)
  - [Try/Catch Cost In a Loop](https://jsperf.com/try-catch-in-loop-cost)
  - [Bang Function](https://jsperf.com/bang-function)
  - [jQuery Find vs Context, Selector](https://jsperf.com/jquery-find-vs-context-sel/13)
  - [innerHTML vs textContent for script text](https://jsperf.com/innerhtml-vs-textcontent-for-script-text)
  - [Long String Concatenation](https://jsperf.com/ya-string-concat)
  - [Are Javascript functions like `map()`, `reduce()`, and `filter()` optimized for traversing arrays?](https://www.quora.com/JavaScript-programming-language-Are-Javascript-functions-like-map-reduce-and-filter-already-optimized-for-traversing-array/answer/Quildreen-Motta)
  - Loading...

**[⬆ 顶部](#内容索引)**

## 资源-Resources

**Learning ES6+**

  - [Latest ECMA spec](https://tc39.github.io/ecma262/)
  - [ExploringJS](http://exploringjs.com/)
  - [ES6 Compatibility Table](https://kangax.github.io/compat-table/es6/)
  - [Comprehensive Overview of ES6 Features](http://es6-features.org/)

**Read This**

  - [Standard ECMA-262](http://www.ecma-international.org/ecma-262/6.0/index.html)

**Tools**

  - Code Style Linters
    - [ESlint](https://eslint.org/) - [Airbnb Style .eslintrc](https://github.com/airbnb/javascript/blob/master/linters/.eslintrc)
    - [JSHint](http://jshint.com/) - [Airbnb Style .jshintrc](https://github.com/airbnb/javascript/blob/master/linters/.jshintrc)
  - Neutrino Preset - [@neutrinojs/airbnb](https://neutrinojs.org/packages/airbnb/)

**Other Style Guides**

  - [Google JavaScript Style Guide](https://google.github.io/styleguide/javascriptguide.xml)
  - [jQuery Core Style Guidelines](https://contribute.jquery.org/style-guide/js/)
  - [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js)
  - [StandardJS](https://standardjs.com)

**Other Styles**

  - [Naming this in nested functions](https://gist.github.com/cjohansen/4135065) - Christian Johansen
  - [Conditional Callbacks](https://github.com/airbnb/javascript/issues/52) - Ross Allen
  - [Popular JavaScript Coding Conventions on GitHub](http://sideeffect.kr/popularconvention/#javascript) - JeongHoon Byun
  - [Multiple var statements in JavaScript, not superfluous](http://benalman.com/news/2012/05/multiple-var-statements-javascript/) - Ben Alman

**Further Reading**

  - [Understanding JavaScript Closures](https://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/) - Angus Croll
  - [Basic JavaScript for the impatient programmer](http://www.2ality.com/2013/06/basic-javascript.html) - Dr. Axel Rauschmayer
  - [You Might Not Need jQuery](http://youmightnotneedjquery.com/) - Zack Bloom & Adam Schwartz
  - [ES6 Features](https://github.com/lukehoban/es6features) - Luke Hoban
  - [Frontend Guidelines](https://github.com/bendc/frontend-guidelines) - Benjamin De Cock

**Books**

  - [JavaScript: The Good Parts](https://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742) - Douglas Crockford
  - [JavaScript Patterns](https://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) - Stoyan Stefanov
  - [Pro JavaScript Design Patterns](https://www.amazon.com/JavaScript-Design-Patterns-Recipes-Problem-Solution/dp/159059908X)  - Ross Harmes and Dustin Diaz
  - [High Performance Web Sites: Essential Knowledge for Front-End Engineers](https://www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309) - Steve Souders
  - [Maintainable JavaScript](https://www.amazon.com/Maintainable-JavaScript-Nicholas-C-Zakas/dp/1449327680) - Nicholas C. Zakas
  - [JavaScript Web Applications](https://www.amazon.com/JavaScript-Web-Applications-Alex-MacCaw/dp/144930351X) - Alex MacCaw
  - [Pro JavaScript Techniques](https://www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273) - John Resig
  - [Smashing Node.js: JavaScript Everywhere](https://www.amazon.com/Smashing-Node-js-JavaScript-Everywhere-Magazine/dp/1119962595) - Guillermo Rauch
  - [Secrets of the JavaScript Ninja](https://www.amazon.com/Secrets-JavaScript-Ninja-John-Resig/dp/193398869X) - John Resig and Bear Bibeault
  - [Human JavaScript](http://humanjavascript.com/) - Henrik Joreteg
  - [Superhero.js](http://superherojs.com/) - Kim Joar Bekkelund, Mads Mobæk, & Olav Bjorkoy
  - [JSBooks](http://jsbooks.revolunet.com/) - Julien Bouquillon
  - [Third Party JavaScript](https://www.manning.com/books/third-party-javascript) - Ben Vinegar and Anton Kovalyov
  - [Effective JavaScript: 68 Specific Ways to Harness the Power of JavaScript](http://amzn.com/0321812182) - David Herman
  - [Eloquent JavaScript](http://eloquentjavascript.net/) - Marijn Haverbeke
  - [You Don’t Know JS: ES6 & Beyond](http://shop.oreilly.com/product/0636920033769.do) - Kyle Simpson

**Blogs**

  - [JavaScript Weekly](http://javascriptweekly.com/)
  - [JavaScript, JavaScript...](https://javascriptweblog.wordpress.com/)
  - [Bocoup Weblog](https://bocoup.com/weblog)
  - [Adequately Good](http://www.adequatelygood.com/)
  - [NCZOnline](https://www.nczonline.net/)
  - [Perfection Kills](http://perfectionkills.com/)
  - [Ben Alman](http://benalman.com/)
  - [Dmitry Baranovskiy](http://dmitry.baranovskiy.com/)
  - [nettuts](http://code.tutsplus.com/?s=javascript)

**Podcasts**

  - [JavaScript Air](https://javascriptair.com/)
  - [JavaScript Jabber](https://devchat.tv/js-jabber/)

**[⬆ 顶部](#内容索引)**

## In the Wild

  This is a list of organizations that are using this style guide. Send us a pull request and we'll add you to the list.

  - **123erfasst**: [123erfasst/javascript](https://github.com/123erfasst/javascript)
  - **3blades**: [3Blades](https://github.com/3blades)
  - **4Catalyzer**: [4Catalyzer/javascript](https://github.com/4Catalyzer/javascript)
  - **Aan Zee**: [AanZee/javascript](https://github.com/AanZee/javascript)
  - **Adult Swim**: [adult-swim/javascript](https://github.com/adult-swim/javascript)
  - **Airbnb**: [airbnb/javascript](https://github.com/airbnb/javascript)
  - **AltSchool**: [AltSchool/javascript](https://github.com/AltSchool/javascript)
  - **Apartmint**: [apartmint/javascript](https://github.com/apartmint/javascript)
  - **Ascribe**: [ascribe/javascript](https://github.com/ascribe/javascript)
  - **Avalara**: [avalara/javascript](https://github.com/avalara/javascript)
  - **Avant**: [avantcredit/javascript](https://github.com/avantcredit/javascript)
  - **Axept**: [axept/javascript](https://github.com/axept/javascript)
  - **BashPros**: [BashPros/javascript](https://github.com/BashPros/javascript)
  - **Billabong**: [billabong/javascript](https://github.com/billabong/javascript)
  - **Bisk**: [bisk](https://github.com/Bisk/)
  - **Bonhomme**: [bonhommeparis/javascript](https://github.com/bonhommeparis/javascript)
  - **Brainshark**: [brainshark/javascript](https://github.com/brainshark/javascript)
  - **CaseNine**: [CaseNine/javascript](https://github.com/CaseNine/javascript)
  - **Cerner**: [Cerner](https://github.com/cerner/)
  - **Chartboost**: [ChartBoost/javascript-style-guide](https://github.com/ChartBoost/javascript-style-guide)
  - **ComparaOnline**: [comparaonline/javascript](https://github.com/comparaonline/javascript-style-guide)
  - **Compass Learning**: [compasslearning/javascript-style-guide](https://github.com/compasslearning/javascript-style-guide)
  - **DailyMotion**: [dailymotion/javascript](https://github.com/dailymotion/javascript)
  - **DoSomething**: [DoSomething/eslint-config](https://github.com/DoSomething/eslint-config)
  - **Digitpaint** [digitpaint/javascript](https://github.com/digitpaint/javascript)
  - **Drupal**: [www.drupal.org](https://www.drupal.org/project/drupal)
  - **Ecosia**: [ecosia/javascript](https://github.com/ecosia/javascript)
  - **Evernote**: [evernote/javascript-style-guide](https://github.com/evernote/javascript-style-guide)
  - **Evolution Gaming**: [evolution-gaming/javascript](https://github.com/evolution-gaming/javascript)
  - **EvozonJs**: [evozonjs/javascript](https://github.com/evozonjs/javascript)
  - **ExactTarget**: [ExactTarget/javascript](https://github.com/ExactTarget/javascript)
  - **Expensify** [Expensify/Style-Guide](https://github.com/Expensify/Style-Guide/blob/master/javascript.md)
  - **Flexberry**: [Flexberry/javascript-style-guide](https://github.com/Flexberry/javascript-style-guide)
  - **Gawker Media**: [gawkermedia](https://github.com/gawkermedia/)
  - **General Electric**: [GeneralElectric/javascript](https://github.com/GeneralElectric/javascript)
  - **Generation Tux**: [GenerationTux/javascript](https://github.com/generationtux/styleguide)
  - **GoodData**: [gooddata/gdc-js-style](https://github.com/gooddata/gdc-js-style)
  - **GreenChef**: [greenchef/javascript](https://github.com/greenchef/javascript)
  - **Grooveshark**: [grooveshark/javascript](https://github.com/grooveshark/javascript)
  - **Grupo-Abraxas**: [Grupo-Abraxas/javascript](https://github.com/Grupo-Abraxas/javascript)
  - **Honey**: [honeyscience/javascript](https://github.com/honeyscience/javascript)
  - **How About We**: [howaboutwe/javascript](https://github.com/howaboutwe/javascript-style-guide)
  - **Huballin**: [huballin](https://github.com/huballin/)
  - **HubSpot**: [HubSpot/javascript](https://github.com/HubSpot/javascript)
  - **Hyper**: [hyperoslo/javascript-playbook](https://github.com/hyperoslo/javascript-playbook/blob/master/style.md)
  - **InterCity Group**: [intercitygroup/javascript-style-guide](https://github.com/intercitygroup/javascript-style-guide)
  - **Jam3**: [Jam3/Javascript-Code-Conventions](https://github.com/Jam3/Javascript-Code-Conventions)
  - **JeopardyBot**: [kesne/jeopardy-bot](https://github.com/kesne/jeopardy-bot/blob/master/STYLEGUIDE.md)
  - **JSSolutions**: [JSSolutions/javascript](https://github.com/JSSolutions/javascript)
  - **Kaplan Komputing**: [kaplankomputing/javascript](https://github.com/kaplankomputing/javascript)
  - **KickorStick**: [kickorstick](https://github.com/kickorstick/)
  - **Kinetica Solutions**: [kinetica/javascript](https://github.com/kinetica/Javascript-style-guide)
  - **LEINWAND**: [LEINWAND/javascript](https://github.com/LEINWAND/javascript)
  - **Lonely Planet**: [lonelyplanet/javascript](https://github.com/lonelyplanet/javascript)
  - **M2GEN**: [M2GEN/javascript](https://github.com/M2GEN/javascript)
  - **Mighty Spring**: [mightyspring/javascript](https://github.com/mightyspring/javascript)
  - **MinnPost**: [MinnPost/javascript](https://github.com/MinnPost/javascript)
  - **MitocGroup**: [MitocGroup/javascript](https://github.com/MitocGroup/javascript)
  - **ModCloth**: [modcloth/javascript](https://github.com/modcloth/javascript)
  - **Money Advice Service**: [moneyadviceservice/javascript](https://github.com/moneyadviceservice/javascript)
  - **Muber**: [muber](https://github.com/muber/)
  - **National Geographic**: [natgeo](https://github.com/natgeo/)
  - **Nimbl3**: [nimbl3/javascript](https://github.com/nimbl3/javascript)
  - **NullDev**: [NullDevCo/JavaScript-Styleguide](https://github.com/NullDevCo/JavaScript-Styleguide)
  - **Nulogy**: [nulogy/javascript](https://github.com/nulogy/javascript)
  - **Orange Hill Development**: [orangehill/javascript](https://github.com/orangehill/javascript)
  - **Orion Health**: [orionhealth/javascript](https://github.com/orionhealth/javascript)
  - **OutBoxSoft**: [OutBoxSoft/javascript](https://github.com/OutBoxSoft/javascript)
  - **Peerby**: [Peerby/javascript](https://github.com/Peerby/javascript)
  - **Pier 1**: [Pier1/javascript](https://github.com/pier1/javascript)
  - **Qotto**: [Qotto/javascript-style-guide](https://github.com/Qotto/javascript-style-guide)
  - **Razorfish**: [razorfish/javascript-style-guide](https://github.com/razorfish/javascript-style-guide)
  - **reddit**: [reddit/styleguide/javascript](https://github.com/reddit/styleguide/tree/master/javascript)
  - **React**: [facebook.github.io/react/contributing/how-to-contribute.html#style-guide](https://facebook.github.io/react/contributing/how-to-contribute.html#style-guide)
  - **REI**: [reidev/js-style-guide](https://github.com/rei/code-style-guides/)
  - **Ripple**: [ripple/javascript-style-guide](https://github.com/ripple/javascript-style-guide)
  - **Sainsbury’s Supermarkets**: [jsainsburyplc](https://github.com/jsainsburyplc)
  - **SeekingAlpha**: [seekingalpha/javascript-style-guide](https://github.com/seekingalpha/javascript-style-guide)
  - **Shutterfly**: [shutterfly/javascript](https://github.com/shutterfly/javascript)
  - **Sourcetoad**: [sourcetoad/javascript](https://github.com/sourcetoad/javascript)
  - **Springload**: [springload](https://github.com/springload/)
  - **StratoDem Analytics**: [stratodem/javascript](https://github.com/stratodem/javascript)
  - **SteelKiwi Development**: [steelkiwi/javascript](https://github.com/steelkiwi/javascript)
  - **StudentSphere**: [studentsphere/javascript](https://github.com/studentsphere/guide-javascript)
  - **SwoopApp**: [swoopapp/javascript](https://github.com/swoopapp/javascript)
  - **SysGarage**: [sysgarage/javascript-style-guide](https://github.com/sysgarage/javascript-style-guide)
  - **Syzygy Warsaw**: [syzygypl/javascript](https://github.com/syzygypl/javascript)
  - **Target**: [target/javascript](https://github.com/target/javascript)
  - **Terra**: [terra](https://github.com/cerner?utf8=%E2%9C%93&q=terra&type=&language=)
  - **TheLadders**: [TheLadders/javascript](https://github.com/TheLadders/javascript)
  - **The Nerdery**: [thenerdery/javascript-standards](https://github.com/thenerdery/javascript-standards)
  - **T4R Technology**: [T4R-Technology/javascript](https://github.com/T4R-Technology/javascript)
  - **UrbanSim**: [urbansim](https://github.com/urbansim/)
  - **VoxFeed**: [VoxFeed/javascript-style-guide](https://github.com/VoxFeed/javascript-style-guide)
  - **WeBox Studio**: [weboxstudio/javascript](https://github.com/weboxstudio/javascript)
  - **Weggo**: [Weggo/javascript](https://github.com/Weggo/javascript)
  - **Zillow**: [zillow/javascript](https://github.com/zillow/javascript)
  - **ZocDoc**: [ZocDoc/javascript](https://github.com/ZocDoc/javascript)

**[⬆ 顶部](#内容索引)**

## Translation

  This style guide is also available in other languages:

  - ![br](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Brazilian Portuguese**: [armoucar/javascript-style-guide](https://github.com/armoucar/javascript-style-guide)
  - ![bg](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Bulgaria.png) **Bulgarian**: [borislavvv/javascript](https://github.com/borislavvv/javascript)
  - ![ca](https://raw.githubusercontent.com/fpmweb/javascript-style-guide/master/img/catala.png) **Catalan**: [fpmweb/javascript-style-guide](https://github.com/fpmweb/javascript-style-guide)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [lin-123/javascript](https://github.com/lin-123/javascript)
  - ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Chinese (Traditional)**: [jigsawye/javascript](https://github.com/jigsawye/javascript)
  - ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **French**: [nmussy/javascript-style-guide](https://github.com/nmussy/javascript-style-guide)
  - ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **German**: [timofurrer/javascript-style-guide](https://github.com/timofurrer/javascript-style-guide)
  - ![it](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**: [sinkswim/javascript-style-guide](https://github.com/sinkswim/javascript-style-guide)
  - ![jp](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [mitsuruog/javascript-style-guide](https://github.com/mitsuruog/javascript-style-guide)
  - ![kr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [ParkSB/javascript-style-guide](https://github.com/ParkSB/javascript-style-guide)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**: [leonidlebedev/javascript-airbnb](https://github.com/leonidlebedev/javascript-airbnb)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [paolocarrasco/javascript-style-guide](https://github.com/paolocarrasco/javascript-style-guide)
  - ![th](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Thailand.png) **Thai**: [lvarayut/javascript-style-guide](https://github.com/lvarayut/javascript-style-guide)
  - ![tr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Turkey.png) **Turkish**: [eraycetinay/javascript](https://github.com/eraycetinay/javascript)
  - ![ua](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Ukraine.png) **Ukrainian**: [ivanzusko/javascript](https://github.com/ivanzusko/javascript)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnam**: [hngiang/javascript-style-guide](https://github.com/hngiang/javascript-style-guide)

## The JavaScript Style Guide Guide

  - [Reference](https://github.com/airbnb/javascript/wiki/The-JavaScript-Style-Guide-Guide)

## Chat With Us About JavaScript

  - Find us on [gitter](https://gitter.im/airbnb/javascript).

## Contributors

  - [View Contributors](https://github.com/airbnb/javascript/graphs/contributors)

## License

(The MIT License)

Copyright (c) 2012 Airbnb

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ 顶部](#内容索引)**

## Amendments

We encourage you to fork this guide and change the rules to fit your team’s style guide. Below, you may list some amendments to the style guide. This allows you to periodically update your style guide without having to deal with merge conflicts.

# };