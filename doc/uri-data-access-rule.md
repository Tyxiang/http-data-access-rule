# URI 数据访问规则 uri data access rule

## 1. 概述 Introduction

这是一套 URI 访问结构化数据、半结构化数据的方法。

## 2. 术语和定义 Terms and definitions

#### 2.1. 结构化数据 structured data

#### 2.2. 半结构化数据 semi-structured data

#### 2.3. 基于文本的半结构化数据描述语言 text-based semi-structured data description language

如：json、yaml、xml

#### 2.4. 键 Key

#### 2.5. 值 Value

#### 2.6. 有序值列表（列表）OVL

#### 2.7. 键值对集合（集合）KVS

#### 2.8. 标量 SV

## 3. 符号与缩略语

变量 {n}

## 4. URI 中的符号 Symbols in URI

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

## 5. 基本访问 Basic Access

### 5.1. KVS

| URI                  | 语义           | 其他 |
| -------------------- | -------------- | ---- |
| `/{key}/`            | 访问键；       |      |
| `/{key}`             | 访问值；       |      |
| `/{key}/.{property}` | 访问键的属性； |      |
| `/{key}.{property}`  | 访问值的属性； |      |

### 5.2. OVL

| URI                           | 语义                 | 其他 |
| ----------------------------- | -------------------- | ---- |
| `/{key}()/`                   | 访问键；             |      |
| `/{key}()`                    | 访问值；             |      |
| `/{key}({index})/`            | 访问成员的键；       |      |
| `/{key}({index})`             | 访问成员的值；       |      |
| `/{key}()/.{property}`        | 访问键的属性；       |      |
| `/{key}().{property}`         | 访问值的属性；       |      |
| `/{key}({index})/.{property}` | 访问成员的键的属性； |      |
| `/{key}({index}).{property}`  | 访问成员的值的属性;  |      |

## 6. OVL 结果集的查询 Query

### 6.1. 方法

#### 6.1.1. 过滤

<kbd>*格式*</kbd>

```
filter({key},{cmpr},{value})
```

<kbd>*说明*</kbd>

- 比较符 cmpr

| 符号 | 语义     |
| ---- | -------- |
| `eq` | 等于     |
| `eq` | 等于     |
| `ne` | 不等于   |
| `gt` | 大于     |
| `lt` | 小于     |
| `ge` | 大于等于 |
| `le` | 小于等于 |

<kbd>*示例*</kbd>

```
?q=filter(id,eq,'0001')   // 过滤出 id 等于 '0001' 的项
?q=filter(age,ge,20)      // 过滤出 age 大于等于 20 的项
```

#### 6.1.2. 搜索

<kbd>*格式*</kbd>

```
search({key},{keyword})
search({key},{keyword1},{keyword2})
search({key},{keyword1},{keyword2},{keyword3},...)
```

<kbd>*说明*</kbd>

- 逗号分开的关键词之间为“或”关系；

<kbd>*示例*</kbd>

```
?q=search(name,Tom,Jarry)   // 搜索 name 中包含 Tom 或 Jerry 的项
```

#### 6.1.3. 去除

<kbd>*格式*</kbd>

```
except({key},{keyword})
except({key},{keyword1},{keyword2})
except({key},{keyword1},{keyword2},{keyword3},...)
```

<kbd>*说明*</kbd>

- 逗号分开的关键词之间为“或”关系；

<kbd>*示例*</kbd>

```
?q=except(name,Tom,Jarry)   // 去除 name 中包含 Tom 或 Jerry 的项
```

#### 6.1.4. 排序

<kbd>*格式*</kbd>

```
orderby({way},{key1})
orderby({way},{key1},{key2})
orderby({way},{key1},{key2},{key3},...)
```

<kbd>*说明*</kbd>

- `way` 有两个选项 `asc` 从小到大、`des` 从大到小；
- 排序时前面的 key 优先；

<kbd>*示例*</kbd>

```
?q=orderby(asc,name,age)    // 从小到大排列，name 优先，age 其次
```

#### 6.1.5. 选择列

<kbd>*格式*</kbd>

```
select({key})
select({key1},{key2})
select({key1},{key2},{key3},...)
```

<kbd>*示例*</kbd>

```
?q=select(name,age)  // 选择 name 和 age 两列
```

#### 6.1.6. 返回所有键

<kbd>*格式*</kbd>

```
keys()
```

<kbd>*示例*</kbd>

```
?q=keys()
```

#### 6.1.7. 返回所有值

<kbd>*格式*</kbd>

```
values()
```

<kbd>*示例*</kbd>

```
?q=values()
```

<!--

#### 6.1.8. 获取前 n 项

<kbd>*格式*</kbd>

```
top({n})
```

<kbd>*示例*</kbd>

```
?q=top(10)  // 获取前十项
```

#### 6.1.9. 获取后 n 项

<kbd>*格式*</kbd>

```
last({n})
```

<kbd>*示例*</kbd>

```
?q=last(10)  // 获取后十项
```
-->

#### 6.1.10. 截取

<kbd>*格式*</kbd>

```
cut({start},{end})
```

<kbd>*说明*</kbd>

- `start` 开始的 index，空表示从 `0` 开始，负数表示倒数；
- `end` 结束的 index，空代表到最后，负数表示倒数；

<kbd>*示例*</kbd>

```
?q=cut(1,5)     // 获取 index 从 1 到 5 的项目；
?q=cut(,5)      // 获取 index 从 0 到 5 的项目；
?q=cut(1,)      // 获取 index 从 1 到最后的项目；
?q=cut(-2,5)    // ？
?q=cut(2,-5)    // ？
?q=cut(-2,-5)   // ？
```

### 6.2. 组合

<kbd>*格式*</kbd>

<kbd>*说明*</kbd>

- 从左到右处理；

<kbd>*示例*</kbd>

```
?q=filter(id,gt,0001)+search(name,Tom)+select(id,name,age)+except(age,20)
?q=filter(id,gt,0001),search(name,Tom,Jarry)+select(id,name,age)+except(age,20)
?q=except(name,Tom)+except(from,beijing) // 去除 name 为 Tom 或 from 为 beijing 的项
?q=except(name,Tom),except(from,beijing) // 去除 name 为 Tom 且 from 为 beijing 的项
?q=search(name,Tom)+search(from,beijing) // 搜索 name 为 Tom 且 from 为 beijing 的项
?q=search(name,Tom),search(from,beijing) // 搜索 name 为 Tom 或 from 为 beijing 的项
```

## 7. OVL 结果集的统计 Statistic

### 7.1. 方法

count()
max(id)
min(price)
avg(price,2)

### 7.2. 组合

<kbd>*格式*</kbd>

<kbd>*说明*</kbd>

- 从左到右处理；

<kbd>*示例*</kbd>

```
?q=filter(id,gt,0001)+search(name,Tom)&s=max()
?q=filter(id,gt,0001),search(name,Tom,Jarry)+select(id,name,age)&s=count()
```

## 8. KVS 通配 Wildcard

### 8.1. 方法

#### 8.1.1. 多字符通配

<kbd>*格式*</kbd>

`*`

<kbd>*说明*</kbd>

<kbd>*示例*</kbd>

`a*`

#### 8.1.2. 单字符通配

`_`；

#### 8.1.3. 任一字符通配

`'b,c,d'`；

#### 8.1.4. 排除

`'!b,!c,!d'`；

### 8.2. 组合
