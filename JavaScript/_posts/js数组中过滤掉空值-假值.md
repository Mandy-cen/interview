---
title: 'js数组中过滤掉空值,假值'
date: 2019-08-29 14:27:42
tags: javaScript
---

利用Array的filter过滤掉数组里的空值假值（false, undefined, NaN, null, 0）

```yaml
arr = [undefined, undefined, 0, 1, '', 'false', false, true, null, 'null']

arr.filter(e => e)

或者

arr.filter(Boolean)

```

结果：`[1, "false", true, "null"]`