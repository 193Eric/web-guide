# 命名规范

## 目的

提高代码可预测性和可维护性的方法是使用命名约定，这就意味着采用一致的方法来对变量和函数进行命名

## 构造函数（类）命名

首字母大写，驼峰式命名。

```js
  let man = new Person();
```

## 变量命名

变量名包括全局变量，局部变量，类变量，函数参数
首字母小写，驼峰式(Camel)命名，匈牙利命名
如：`checkCount` 表示整形的数值

### 常量

使用全部字母大写，单词间下划线分隔的命名方式。

```js
  let HTML_ENTITY = {};
```

### 函数, 函数的参数

使用 Camel 命名法。

```js
  function stringFormat(source) {}
  function hear(theBells) {}
```

### 类相关

类：使用 Pascal 命名法(首字母大写的Camel命名法)
类的 方法 / 属性, 使用 Camel 命名法

```js
  function TextNode(value, engine) {
    this.value = value;
    this.engine = engine;
  }

  TextNode.prototype.clone = function () {
    return this;
  };
```

### 由多个单词组成的 缩写词，在命名中，根据当前命名法和出现的位置，所有字母的大小写与首字母的大小写保持一致。

```js
  function XMLParser() {}

  function insertHTML(element, html) {}

  let httpRequest = new HTTPRequest();
```

## 命名语法

1. 类名，使用名词

```js
  function Engine(options) {}
```

2. 函数名，使用动宾短语

```js
  function getStyle(element) {}
```

3. boolean 类型的变量使用 is 或 has 开头

```js
  let isReady = false;
  let hasMoreCommands = false;
```

4. Promise 对象用动宾短语的进行时表达。

```js
  let loadingData = ajax.get('url');
  loadingData.then(callback);
```

## 例外情况

以根据项目及团队需要，设计出针对项目需要的前缀规范，从而达到团队开发协作便利的目的。
作用域不大临时变量可以简写，比如：`str，num，bol，obj，fun，arr`。
循环变量可以简写，比如：`i，j，k`等。
某些作为不允许修改值的变量认为是常量，全部字母都大写。例如：`COPYRIGHT，PI`。常量可以存在于函数中，也可以存在于全局。必须采用全大写的命名，且单词以_分割，常量通常用于ajax请求url，和一些不会改变的数据。

## 函数命名

1. 普通函数：首字母小写，驼峰式命名，统一使用动词或者动词+名词形式

```js
  getVersion() // 获得版本号
  submitForm() // 提交表单
  init()  // 初始化
```

2. 涉及返回逻辑值的函数可以使用is，has，contains等表示逻辑的词语代替动词

```js
  isObject() // 是否对象
  hasClass('xx') // 有xx对象吗
  containsElment('xx') // 包含xx元素吗
```

3. 事件句柄函数，可以在上面的函数名添加*handler*前缀

```js
  handlerGetVersion()
  handlerSubmitForm()
```

函数方法常用的动词：

```html
get 获取/set 设置,
add 增加/remove 删除
create 创建/destory 移除
start 启动/stop 停止
open 打开/close 关闭,
read 读取/write 写入
load 载入/save 保存,
create 创建/destroy 销毁
begin 开始/end 结束,
backup 备份/restore 恢复
import 导入/export 导出,
split 分割/merge 合并
inject 注入/extract 提取,
attach 附着/detach 脱离
bind 绑定/separate 分离,
view 查看/browse 浏览
edit 编辑/modify 修改,
select 选取/mark 标记
copy 复制/paste 粘贴,
undo 撤销/redo 重做
insert 插入/delete 移除,
add 加入/append 添加
clean 清理/clear 清除,
index 索引/sort 排序
find 查找/search 搜索,
increase 增加/decrease 减少
play 播放/pause 暂停,
launch 启动/run 运行
compile 编译/execute 执行,
debug 调试/trace 跟踪
observe 观察/listen 监听,
build 构建/publish 发布
input 输入/output 输出,
encode 编码/decode 解码
encrypt 加密/decrypt 解密,
compress 压缩/decompress 解压缩
pack 打包/unpack 解包,
parse 解析/emit 生成
connect 连接/disconnect 断开,
send 发送/receive 接收
download 下载/upload 上传,
refresh 刷新/synchronize 同步
update 更新/revert 复原,
lock 锁定/unlock 解锁
check out 签出/check in 签入,
submit 提交/commit 交付
push 推/pull 拉,
expand 展开/collapse 折叠
begin 起始/end 结束,
start 开始/finish 完成
enter 进入/exit 退出,
abort 放弃/quit 离开
obsolete 废弃/depreciate 废旧,
collect 收集/aggregate 聚集
```