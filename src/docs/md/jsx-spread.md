# JSX 展开属性

如果你事先知道组件需要的全部 Props（属性），JSX 很容易地这样写：

```javascript
  var component = <Component foo={x} bar={y} />;
```

## 修改 Props 是不好的，明白吗

如果你不知道要设置哪些 Props，那么现在最好不要设置它：

```javascript
  var component = <Component />;
  component.props.foo = x; // 不好
  component.props.bar = y; // 同样不好
```

这样是反模式，因为 React 不能帮你检查属性类型（propTypes）。这样即使你的 属性类型有错误也不能得到清晰的错误提示。

Props 应该被认为是不可变的。在别处修改 props 对象可能会导致预料之外的结果，所以原则上这将是一个冻结的对象。

## 展开属性（Spread Attributes）

现在你可以使用 JSX 的新特性 - 展开属性：

```javascript
  var props = {};
  props.foo = x;
  props.bar = y;
  var component = <Component {...props} />;
```

传入对象的属性会被复制到组件内。

它能被多次使用，也可以和其它属性一起用。注意顺序很重要，后面的会覆盖掉前面的。

```javascript
  var props = { foo: 'default' };
  var component = <Component {...props} foo={'override'} />;
  console.log(component.props.foo); // 'override'
```

## 这个奇怪的 `...` 标记是什么？

这个 `...` 操作符（增强的操作符）已经被 [ES6 数组](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator) 支持。相关的还有 ECMAScript 规范草案中的 [Object 剩余和展开属性（Rest and Spread Properties）](https://github.com/sebmarkbage/ecmascript-rest-spread)。我们利用了这些还在制定中标准中已经被支持的特性来使 JSX 拥有更优雅的语法。
