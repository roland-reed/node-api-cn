<!-- YAML
added: v0.1.31
changes:
  - version: v12.10.0
    pr-url: https://github.com/nodejs/node/pull/29212
    description: Enable `emitClose` option.
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using
                 `file:` protocol. Support is currently still *experimental*.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7831
    description: The passed `options` object will never be modified.
  - version: v5.5.0
    pr-url: https://github.com/nodejs/node/pull/3679
    description: The `autoClose` option is supported now.
  - version: v2.3.0
    pr-url: https://github.com/nodejs/node/pull/1845
    description: The passed `options` object can be a string now.
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `flags` {string} 参阅[支持的文件系统标志][support of file system `flags`]。**默认值:** `'w'`。
  * `encoding` {string} **默认值:** `'utf8'`。
  * `fd` {integer} **默认值:** `null`。
  * `mode` {integer} **默认值:** `0o666`。
  * `autoClose` {boolean} **默认值:** `true`。
  * `emitClose` {boolean} **默认值:** `false`。
  * `start` {integer}
* 返回: {fs.WriteStream}

`options` 可以包括 `start` 选项，允许在文件的开头之后的某个位置写入数据，允许的值在 [0, [`Number.MAX_SAFE_INTEGER`]] 的范围内。
若要修改文件而不是覆盖它，则 `flags` 模式需要为 `r+` 而不是默认的 `w` 模式。
`encoding` 可以是 [`Buffer`] 接受的任何一种字符编码。

如果 `autoClose` 设置为 `true`（默认的行为），则在 `'error'` 或 `'finish'` 事件时文件描述符将会被自动地关闭。
如果 `autoClose` 为 `false`，则即使出现错误，文件描述符也不会被关闭。
应用程序负责关闭它并确保没有文件描述符泄漏。

默认情况下，流在销毁后将不会触发 `'close'` 事件。 
这与其他 `Writable` 流的默认行为相反。 
将 `emitClose` 选项设置为 `true` 可更改此行为。

与 [`ReadStream`] 类似，如果指定了 `fd`，则 [`WriteStream`] 将会忽略 `path` 参数并将会使用指定的文件描述符。
这意味着不会触发 `'open'` 事件。
`fd` 必须是阻塞的，非阻塞的 `fd` 应该传给 [`net.Socket`]。

如果 `options` 是字符串，则它指定字符编码。

