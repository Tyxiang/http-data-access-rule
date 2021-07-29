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

|  符号   | 作用                         | 语义 | 其他 |
| :-----: | ---------------------------- | ---- | ---- |
|   `/`   | 键间隔符；                   |      |      |
| `(` `)` | 索引访问符；查询参数符；     |      |      |
|   `.`   | 属性方法访问符；             |      |      |
|   `+`   | 取子集符号；                 | 与   |      |
|  `, `   | 参数间隔符；枚举间隔符；     | 或   |      |
| `'` `'` | 字符串标识符；可选集标识符； |      |      |
|   `*`   | 多字符通配符；               |      |      |
|   `_`   | 单字符通配符；               |      |      |
|   `-`   | 切片符；                     | 至   |      |
|   `!`   | 排除符；                     | 非   |      |
|   `$`   |                              |      |      |

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

### 6.1. filter()

**用途** 

对结果进行过滤操作；

**格式**

```
filter({key},{cmpr},{value})
```

**说明**

- 比较符 cmpr

| 符号 | 语义     |
| ---- | -------- |
| eq   | 等于     |
| eq   | 等于     |
| ne   | 不等于   |
| gt   | 大于     |
| lt   | 小于     |
| ge   | 大于等于 |
| le   | 小于等于 |

**示例**

```
?q=filter(id,eq,'0001')   // 过滤 id 等于 '0001' 的项
?q=filter(age,ge,20)      // 过滤 age 大于等于 20 的项
```

### 6.2. search()

**格式**

```
search({key},{keyword})
search({key},{keyword1},{keyword2})
search({key},{keyword1},{keyword2},{keyword3},...)
```

**说明**

- 逗号分开的关键词之间为“或”关系；

**示例**

```
?q=search(name,Tom,Jarry)                   // 搜索 name 为 Tom 或 Jerry 的项
```

### 6.3. except()

**格式**

```
except({key},{keyword})
except({key},{keyword1},{keyword2})
except({key},{keyword1},{keyword2},{keyword3},...)
```

**说明**

- 逗号分开的关键词之间为“或”关系；

**示例**

```
?q=except(name,Tom,Jarry)                   // 去除 name 为 Tom 或 Jerry 的项
```

### 6.4. orderby()

**格式**

```
orderby({way},{key1})
orderby({way},{key1},{key2})
orderby({way},{key1},{key2},{key3},...)
```

**说明**

- `way` 有两个选项 `asc` 从小到大、`des` 从大到小；
- 排在前面的 key 优先；

**示例**

```
?q=orderby(asc,name,age)  // 从小到大排列，name 优先，age 其次
```

### 6.5. top(10)

### 6.6. last(10)

### 6.7. skip(10)

### 6.8. select()

select(id)
select(id,name)
选择 id 和 name

### 6.9. values()

返回所有值

### 6.10. keys()

返回所有键

### 6.11. 组合使用

**示例**

```
?q=filter(id,gt,0001)+search(name,Tom)+select(id,name,age)+except(age,20)
?q=filter(id,gt,0001),search(name,Tom,Jarry)+select(id,name,age)+except(age,20)
?q=except(name,Tom)+except(from,beijing) // 去除 name 为 Tom 或 from 为 beijing 的项
?q=except(name,Tom),except(from,beijing) // 去除 name 为 Tom 且 from 为 beijing 的项
?q=search(name,Tom)+search(from,beijing) // 搜索 name 为 Tom 且 from 为 beijing 的项
?q=search(name,Tom),search(from,beijing) // 搜索 name 为 Tom 或 from 为 beijing 的项
```

**说明**

- ovl only
- 从左到右处理
- 默认返回键和值
- 适用方法
- get
- put
- delete
