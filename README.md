# HTTP 数据访问规则 http data access rule

## 1. 概述 Introduction

这是一套基于 HTTP 协议，以 RESTful 方式访问结构化数据、半结构化数据的方法。

## 2. 符号与缩略语

- `{n}` 代表 `n` 为变量，`n` 的值是变化的；
- `OVL` 有序值列表（列表）；
- `KVS` 键值对集合（集合）；
- `SV` 标量；
- `URI` 资源定位符；

## 3. URI 中的符号 Symbols in URI

|  符号   | 作用                             | 语义 | 其他 |
| :-----: | -------------------------------- | ---- | ---- |
|   `/`   | 键间隔符；                       |      |      |
| `(` `)` | 索引访问符；<br>查询参数符；     |      |      |
|   `.`   | 属性方法访问符；                 |      |      |
|   `+`   | 取子集符号；                     | 与   |      |
|  `, `   | 参数间隔符；<br>枚举间隔符；     | 或   |      |
| `'` `'` | 字符串标识符；<br>可选集标识符； |      |      |
|   `*`   | 多字符通配符；                   |      |      |
|   `_`   | 单字符通配符；                   |      |      |
|   `-`   | 切片符；                         | 至   |      |
|   `!`   | 排除符；                         | 非   |      |
|   `$`   |                                  |      |      |

## 4. 数据的标识 Data Identifying

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

## 5. RESTful 方式访问数据

### 5.1. 请求

- HTTP 操作：

|  方法  | URI                        | 语义                  | 说明 |
| :----: | -------------------------- | --------------------- | ---- |
|  POST  | /{key}                     | KVS 增加值；          |      |
|  POST  | /{key}()                   | OVL 增加成员；        |      |
|  GET   | /{key}                     | 获取值；              |      |
|  GET   | /{key}.{property}          | 获取属性；            |      |
|  GET   | /{key}({index})            | 获取 OVL 成员的值；   |      |
|  GET   | /{key}({index}).{property} | 获取 OVL 成员的属性； |      |
|  PUT   | /{key}                     | 设置值；              |      |
|  PUT   | /{key}.{property}          | 设置属性；            |      |
|  PUT   | /{key}({index})            | 设置 OVL 成员的值；   |      |
|  PUT   | /{key}({index}).{property} | 设置 OVL 成员的属性； |      |
| DELETE | /{key}                     | 删除值；              |      |
| DELETE | /{key}({index})            | 删除 OVL 成员；       |      |

- 通过 Header 申明 Body 中的数据格式，默认为 JSON；

```
Content-Type: application/json; charset=utf-8
Content-type: application/x-yaml; charset=utf-8
Content-type: application/xml; charset=utf-8
Content-type: text/csv; charset=utf-8
Content-type: application/octet-stream; charset=utf-8
Content-type: text/plain; charset=utf-8 （标量）
```

- 通过 Header 申明期望的数据格式，默认为 JSON；

```
Accept-Charset: utf-8
Accept: application/json
Accept: application/x-yaml
Accept: application/xml
Accept: text/csv
Accept: application/octet-stream
Accept: text/plain （标量）
```

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

## 6. 扩展

- [通配扩展](doc/wildcard.md)
- [查询扩展](doc/query.md)
- [统计扩展](doc/statistic.md)
- [组合使用](doc/mix.md)
