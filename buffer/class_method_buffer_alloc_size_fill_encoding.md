<!-- YAML
added: v5.10.0
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18129
    description: Attempting to fill a non-zero length buffer with a zero length
                 buffer triggers a thrown exception.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/17427
    description: Specifying an invalid string for `fill` triggers a thrown
                 exception.
  - version: v8.9.3
    pr-url: https://github.com/nodejs/node/pull/17428
    description: Specifying an invalid string for `fill` now results in a
                 zero-filled buffer.
-->

* `size` {integer} 新 `Buffer` 的所需长度。
* `fill` {string|Buffer|Uint8Array|integer} 用于预填充新 `Buffer` 的值。**默认值:** `0`。
* `encoding` {string} 如果 `fill` 是一个字符串，则这是它的字符编码。**默认值:** `'utf8'`。

分配一个大小为 `size` 字节的新 `Buffer`。
如果 `fill` 为 `undefined`，则用零填充 `Buffer`。

```js
const buf = Buffer.alloc(5);

console.log(buf);
// 打印: <Buffer 00 00 00 00 00>
```

如果 `size` 大于 [`buffer.constants.MAX_LENGTH`] 或小于 0，则抛出 [`ERR_INVALID_OPT_VALUE`]。
如果 `size` 为 0，则创建一个零长度的 `Buffer`。

如果指定了 `fill`，则分配的 `Buffer` 通过调用 [`buf.fill(fill)`][`buf.fill()`] 进行初始化。

```js
const buf = Buffer.alloc(5, 'a');

console.log(buf);
// 打印: <Buffer 61 61 61 61 61>
```

如果同时指定了 `fill` 和 `encoding`，则分配的 `Buffer` 通过调用 [`buf.fill(fill, encoding)`][`buf.fill()`] 进行初始化 。

```js
const buf = Buffer.alloc(11, 'aGVsbG8gd29ybGQ=', 'base64');

console.log(buf);
// 打印: <Buffer 68 65 6c 6c 6f 20 77 6f 72 6c 64>
```

调用 [`Buffer.alloc()`] 可能比替代的 [`Buffer.allocUnsafe()`] 慢得多，但能确保新创建的 `Buffer` 实例的内容永远不会包含敏感的数据。

如果 `size` 不是一个数字，则抛出 `TypeError`。


