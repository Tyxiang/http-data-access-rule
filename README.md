# HTTP Data Access Rule

## 1. Introduction

This is a set of methods for accessing structured and semi-structured data using the HTTP protocol.

## 2. Symbols

- In the format description, `{n}` means that `n` is a variable.

<!--
- Symbols in URI：

| Symbol  | Effect                           | Other |
| :-----: | -------------------------------- | ----- |
|   `/`   | Spacer between keys              |       |
| `(` `)` | 索引访问；<br>函数参数；         |       |
|   `.`   | 访问属性、方法；<br>访问结果集； |       |
|   `+`   | 集合求并；                       |       |
|   `-`   | 集合求差；                       |       |
|  `, `   | 参数间隔；<br>枚举间隔；         |       |
| `'` `'` | 可选集标识；                     |       |
|   `*`   | 多字符通配；                     |       |
|   `_`   | 单字符通配；                     |       |
|   `!`   | 排除；<br>非；                   |       |
|   `$`   |                                  |       |

-->

## 3. Abbreviations

- `OVL` Ordered values list.
- `KVS` Key-value set.
- `SV` Scalar.
- `URI` Uniform Resource Identifiers.

## 4. Identify data with URI

### 4.1. KVS

| URI                 | Semantic        | Other |
| ------------------- | --------------- | ----- |
| `/{key}`            | Value of KVS    |       |
| `/{key}.{property}` | Property of KVS |       |

### 4.2. OVL

| URI                          | Semantic                     | Other |
| ---------------------------- | ---------------------------- | ----- |
| `/{key}`                     | Value of OVL                 |       |
| `/{key}()`                   | All members of OVL           |       |
| `/{key}({index})`            | The value of a OVL member    |       |
| `/{key}({index}).{property}` | The property of a OVL member |       |

## 5. Access data by HTTP

### 5.1. Request

- Operating data：

| Method | URI                          | Semantic                         | Other |
| :----: | ---------------------------- | -------------------------------- | ----- |
|  POST  | `/{key}`                     | Add value to KVS                 |       |
|  POST  | `/{key}()`                   | Add member to OVL                |       |
|  GET   | `/{key}`                     | Get value                        |       |
|  GET   | `/{key}.{property}`          | Get property                     |       |
|  GET   | `/{key}({index})`            | Get the value of a OVL member    |       |
|  GET   | `/{key}({index}).{property}` | Get the property of a OVL member |       |
|  PUT   | `/{key}`                     | Set value                        |       |
|  PUT   | `/{key}.{property}`          | Set property                     |       |
|  PUT   | `/{key}({index})`            | Set the value of a OVL member    |       |
|  PUT   | `/{key}({index}).{property}` | Set the property of a OVL member |       |
| DELETE | `/{key}`                     | Delete a value                   |       |
| DELETE | `/{key}({index})`            | Delete a OVL member              |       |

- Use Header to declare the data format (the default is JSON):

| Header                                   | Format |
| ---------------------------------------- | ------ |
| `Content-Type: application/json`         | JSON   |
| `Content-type: application/x-yaml`       | YAML   |
| `Content-type: application/xml`          | XML    |
| `Content-type: text/csv`                 | CSV    |
| `Content-type: application/octet-stream` | BIN    |
| `Content-type: text/plain`               | BV     |

- Use Header to declare the expected data format (the default is JSON):

| Header                             | Format |
| ---------------------------------- | ------ |
| `Accept: application/json`         | JSON   |
| `Accept: application/x-yaml`       | YAML   |
| `Accept: application/xml`          | XML    |
| `Accept: text/csv`                 | CSV    |
| `Accept: application/octet-stream` | BIN    |
| `Accept: text/plain`               | BV     |

### 5.2. Response

- Use Header to declare the data format (the default is JSON):
- Successful response: 

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

- Failure response:

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

## 6. URI expansion

- [URI wildcard](doc/wildcard.md)

## 7. Parameter expansion

- [Query the OVL result](doc/query.md)
- [Statistic on the OVL result](doc/statistic.md)
- [Mix using](doc/mixing.md)
