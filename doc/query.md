# OVL 结果集的查询 Query

## 1. 方法

### 1.1. 过滤

<kbd>格式</kbd>

```
filter({key},{cmpr},{value})
```

<kbd>说明</kbd>

- `cmpr` 比较符：

| 符号 | 语义     |
| ---- | -------- |
| `eq` | 等于     |
| `eq` | 等于     |
| `ne` | 不等于   |
| `gt` | 大于     |
| `lt` | 小于     |
| `ge` | 大于等于 |
| `le` | 小于等于 |

<kbd>示例</kbd>

```
?q=filter(id,eq,'0001')   // 过滤出 id 等于 '0001' 的项
?q=filter(age,ge,20)      // 过滤出 age 大于等于 20 的项
```

### 1.2. 搜索

<kbd>格式</kbd>

```
search({key},{keyword})
search({key},{keyword1},{keyword2})
search({key},{keyword1},{keyword2},{keyword3},...)
```

<kbd>说明</kbd>

- 关键词之间为“或”的关系；

<kbd>示例</kbd>

```
?q=search(name,Tom,Jarry)   // 搜索 name 中包含 Tom 或 Jerry 的项
```

### 1.3. 去除

<kbd>格式</kbd>

```
except({key},{keyword})
except({key},{keyword1},{keyword2})
except({key},{keyword1},{keyword2},{keyword3},...)
```

<kbd>说明</kbd>

- 关键词之间为“或”的关系；

<kbd>示例</kbd>

```
?q=except(name,Tom,Jarry)   // 去除 name 中包含 Tom 或 Jerry 的项
```

### 1.4. 排序

<kbd>格式</kbd>

```
orderby({way},{key1})
orderby({way},{key1},{key2})
orderby({way},{key1},{key2},{key3},...)
```

<kbd>说明</kbd>

- `way` 有两个选项 `asc` 从小到大、`des` 从大到小；
- 排序时前面的 key 优先；

<kbd>示例</kbd>

```
?q=orderby(asc,name,age)    // 从小到大排列，name 优先，age 其次
```

### 1.5. 选择列

<kbd>格式</kbd>

```
select({key})
select({key1},{key2})
select({key1},{key2},{key3},...)
```

<kbd>示例</kbd>

```
?q=select(name,age)  // 选择 name 和 age 两列
```

### 1.6. 返回所有键

<kbd>格式</kbd>

```
keys()
```

<kbd>示例</kbd>

```
?q=keys()
```

### 1.7. 返回所有值

<kbd>格式</kbd>

```
values()
```

<kbd>示例</kbd>

```
?q=values()
```

### 1.8. 截取

<kbd>格式</kbd>

```
cut({start},{end})
```

<kbd>说明</kbd>

- `start` 开始的 index，空表示从 `0` 开始，负数表示倒数；
- `end` 结束的 index，空代表到最后，负数表示倒数；

<kbd>示例</kbd>

```
?q=cut(1,5)     // 获取 index 从 1 到 5 的项目；
?q=cut(,5)      // 获取 index 从 0 到 5 的项目；
?q=cut(1,)      // 获取 index 从 1 到最后的项目；
?q=cut(-2,5)    // ？
?q=cut(2,-5)    // ？
?q=cut(-2,-5)   // ？
```
