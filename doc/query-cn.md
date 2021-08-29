# 查询 OVL 结果集

## 1. 查询方法

### 1.1. 过滤

📌 格式

```
filter({key},{cmpr},{value})
```

📌 说明

- `cmpr` 比较符：

| 符号 | 语义     |
| ---- | -------- |
| `eq` | 等于     |
| `ne` | 不等于   |
| `gt` | 大于     |
| `lt` | 小于     |
| `ge` | 大于等于 |
| `le` | 小于等于 |
| `lk` | 近似     |

- 多个过滤可以组合使用：

| 组合符 | 作用     |
| :----: | -------- |
|  `+`   | 取合集   |
|  `-`   | 集合做差 |

📌 示例

```
?q=filter(id,eq,'0001')   // 过滤出 id 等于 '0001' 的项
?q=filter(age,ge,20)      // 过滤出 age 大于等于 20 的项
?q=filter(name,lk,'tom')  // 过滤出 name 近似 tom 的项
?q=filter(id,gt,0005)-filter(name,lk,Tom)
?q=filter(age,gt,15)+filter(name,lk,Tom)
```

### 1.4. 排序

📌 格式

```
order({way},{key1})
order({way},{key1},{key2})
order({way},{key1},{key2},{key3},...)
```

📌 说明

- `way` 有两个选项 `asc` 从小到大、`des` 从大到小；
- 排序时左侧的 key 优先；

📌 示例

```
?q=order(asc,name,age)    // 从小到大排列，name 优先，age 其次
```

### 1.5. 选择列

📌 格式

```
select({key})
select({key1},{key2})
select({key1},{key2},{key3},...)
```

📌 示例

```
?q=select(name,age)  // 选择 name 和 age 两列
```

### 1.6. 获取键

📌 格式

```
keys()
```

📌 说明

- 返回所有键；

📌 示例

```
?q=keys()
```

### 1.7. 获取值

📌 格式

```
values()
```

📌 说明

- 返回所有值；

📌 示例

```
?q=values()
```

### 1.8. 切片

📌 格式

```
cut({start},{end})
cut({start})
cut({start},)
cut(,{end})
cut(,)
```

📌 说明

- `start` 开始的 index；
- `end` 结束的 index；
- index 可以是负数；

📌 示例

|         |  a  |  b  |  c  |  d  |  e  |  f  |
| :-----: | :-: | :-: | :-: | :-: | :-: | :-: |
| index + |  0  |  1  |  2  |  3  |  4  |  5  |
| index - | -6  | -5  | -4  | -3  | -2  | -1  |

```
?q=cut(3)       // d
?q=cut(-2)      // e
?q=cut(1,3)     // b c d
?q=cut(,3)      // a b c d
?q=cut(3,)      // d e f
?q=cut(-5,2)    // b c
?q=cut(2,-5)    // c b
?q=cut(-2,-5)   // e d c b
```

## 2. 查询方法的组合

📌 说明

- 查询方法可以组合使用，组合符为 `.`；
- 组合被从左到右处理，左侧的输出是右侧的输入；

📌 示例

```
?q=filter(id,gt,0001)-filter(name,lk,Tom).select(id,name,age)
?q=filter(id,gt,0001)+filter(name,lk,Tom).select(id,name,age).order(asc,age,name)
?q=select(id,name,age).filter(id,gt,0005)-filter(name,lk,tom).order(asc,age,name).keys().cut(2,)
```
