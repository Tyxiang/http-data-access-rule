# HTTP 数据访问规则

## 1. 概述

这是一套基于 HTTP 协议，以 RESTful 方式访问结构化数据、半结构化数据的方法。

## 2. 符号

- 在格式描述中，`{n}` 表示 `n` 是个变量。

<!--
- URI 中的符号 Symbols in URI：

|  符号   | 作用                             | 其他 |
| :-----: | -------------------------------- | ---- |
|   `/`   | 键之间的间隔符                   |      |
| `(` `)` | 索引访问；<br>函数参数；         |      |
|   `.`   | 访问属性、方法；<br>访问结果集； |      |
|   `+`   | 集合求并；                       |      |
|   `-`   | 集合求差；                       |      |
|  `, `   | 参数间隔；<br>枚举间隔；         |      |
| `'` `'` | 可选集标识；                     |      |
|   `*`   | 多字符通配；                     |      |
|   `_`   | 单字符通配；                     |      |
|   `!`   | 排除；<br>非；                   |      |
|   `$`   |                                  |      |

-->

## 3. 缩略语

- `OVL` 有序值列表；
- `KVS` 键值对集合；
- `SC` 标量；
- `URI` 统一资源标识符；

## 4. 用 URI 标识数据

### 4.1. KVS

| URI                 | 语义         | 其他 |
| ------------------- | ------------ | ---- |
| `/{key}`            | KVS 的值；   |      |
| `/{key}.{property}` | KVS 的属性； |      |

### 4.2. OVL

| URI                          | 语义             | 其他 |
| ---------------------------- | ---------------- | ---- |
| `/{key}`                     | OVL 的值；       |      |
| `/{key}()`                   | OVL 的所有成员； |      |
| `/{key}({index})`            | OVL 成员的值；   |      |
| `/{key}({index}).{property}` | OVL 成员的属性;  |      |

## 5. 用 HTTP 访问数据

### 5.1. 请求

- 操作数据：

|  方法  | URI                          | 语义                  | 说明 |
| :----: | ---------------------------- | --------------------- | ---- |
|  POST  | `/{key}`                     | KVS 增加值；          |      |
|  POST  | `/{key}()`                   | OVL 增加成员；        |      |
|  GET   | `/{key}`                     | 获取值；              |      |
|  GET   | `/{key}.{property}`          | 获取属性；            |      |
|  GET   | `/{key}({index})`            | 获取 OVL 成员的值；   |      |
|  GET   | `/{key}({index}).{property}` | 获取 OVL 成员的属性； |      |
|  PUT   | `/{key}`                     | 设置值；              |      |
|  PUT   | `/{key}.{property}`          | 设置属性；            |      |
|  PUT   | `/{key}({index})`            | 设置 OVL 成员的值；   |      |
|  PUT   | `/{key}({index}).{property}` | 设置 OVL 成员的属性； |      |
| DELETE | `/{key}`                     | 删除值；              |      |
| DELETE | `/{key}({index})`            | 删除 OVL 成员；       |      |

- 通过 Header 申明 Body 中的数据格式（默认为 JSON）：

| Header                                   | 格式 |
| ---------------------------------------- | ---- |
| `Content-Type: application/json`         | JSON |
| `Content-type: application/x-yaml`       | YAML |
| `Content-type: application/xml`          | XML  |
| `Content-type: text/csv`                 | CSV  |
| `Content-type: application/octet-stream` | BIN  |
| `Content-type: text/plain`               | SC   |

- 通过 Header 申明期望的数据格式（默认为 JSON）：

| Header                             | 格式 |
| ---------------------------------- | ---- |
| `Accept: application/json`         | JSON |
| `Accept: application/x-yaml`       | YAML |
| `Accept: application/xml`          | XML  |
| `Accept: text/csv`                 | CSV  |
| `Accept: application/octet-stream` | BIN  |
| `Accept: text/plain`               | SC   |

### 5.2. 响应

- 通过 Header 申明 HTTP Body 中的数据格式，默认为 JSON；
- 成功响应：

```python
# JSON
{
  "success": true,
  "data": "..."
}
```

```yaml
# YAML
success: true
data: ...
```

- 失败响应：

```python
# JSON
{
  "success": false,
  "message": "..."
}
```

```yaml
# YAML
success: false
message: "..."
```

## 6. URI 扩展

- [URI 的通配](doc/wildcard.md)

## 7. 参数扩展

- [OVL 结果集的查询](doc/query.md)
- [OVL 结果集的统计](doc/statistic.md)
- [混合使用](doc/mixing.md)
