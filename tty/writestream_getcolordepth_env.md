<!-- YAML
added: v9.9.0
-->

* `env` {Object} 包含需要检查的环境变量的对象。这使得能够模拟特定终端的使用。**默认值:** `process.env`。
* 返回: {number}

返回:
* `1` 支持 2 种颜色，
* `4` 支持 16 种颜色，
* `8` 支持 256 种颜色，
* `24` 支持 16,777,216 种颜色，

使用此函数可检测终端支持的颜色。
鉴于终端中颜色的特性，可能存在假的正数或假的负数。
这取决于进程信息与环境变量（可能会隐瞒使用的终端）。
可以传入 `env` 对象来模拟特定终端的使用。 
这对于检查特定环境设置的行为方式非常有用。

要强制执行特定的颜色支持，则使用以下环境设置之一。

* 2 种颜色: `FORCE_COLOR = 0` (禁用颜色)
* 16 种颜色: `FORCE_COLOR = 1`
* 256 种颜色: `FORCE_COLOR = 2`
* 16,777,216 种颜色: `FORCE_COLOR = 3`

使用 `NO_COLOR` 和 `NODE_DISABLE_COLORS` 环境变量也可以禁用颜色支持。

