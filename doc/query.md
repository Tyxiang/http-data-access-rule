# OVL 结果集的查询 Query

## 1. 查询方法

### 1.1. 过滤

<kbd>格式</kbd>

```
filter({key},{cmpr},{value})
```

<kbd>说明</kbd>

- `cmpr` 比较符：

| 符号 | 语义        |
| ---- | ----------- |
| `eq` | 等于        |
| `ne` | 不等于      |
| `gt` | 大于        |
| `lt` | 小于        |
| `ge` | 大于等于    |
| `le` | 小于等于    |
| `lk` | 近似        |

- 多个过滤可以组合使用：

| 组合符 | 作用   | 
| :----: | ------ | 
|  `+`   | 取合集 | 
|  `-`   | 取子集 | 

<kbd>示例</kbd>

```
?q=filter(id,eq,'0001')   // 过滤出 id 等于 '0001' 的项
?q=filter(age,ge,20)      // 过滤出 age 大于等于 20 的项
?q=filter(name,lk,'tom')  // 过滤出 name 近似 tom 的项
?q=filter(id,gt,0005)-filter(name,lk,Tom)
?q=filter(age,gt,15)+filter(name,lk,Tom)
```

### 1.4. 排序

<kbd>格式</kbd>

```
order({way},{key1})
order({way},{key1},{key2})
order({way},{key1},{key2},{key3},...)
```

<kbd>说明</kbd>

- `way` 有两个选项 `asc` 从小到大、`des` 从大到小；
- 排序时前面的 key 优先；

<kbd>示例</kbd>

```
?q=order(asc,name,age)    // 从小到大排列，name 优先，age 其次
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

### 1.6. 获取键

<kbd>格式</kbd>

```
keys()
```

<kbd>说明</kbd>

- 返回所有键；

<kbd>示例</kbd>

```
?q=keys()
```

### 1.7. 获取值

<kbd>格式</kbd>

```
values()
```

<kbd>说明</kbd>

- 返回所有值；

<kbd>示例</kbd>

```
?q=values()
```

### 1.8. 切片

<kbd>格式</kbd>

```
cut({start},{end})
cut({start})
cut({start},)
cut(,{end})
cut(,)
```

<kbd>说明</kbd>

- `start` 开始的 index，可以是负数；
- `end` 结束的 index，可以是负数；

<kbd>示例</kbd>

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

<kbd>说明</kbd>

- 查询方法可以组合使用，组合符为 `.`；
- 组合被从左到右处理，左侧的输出是右侧的输入；

<kbd>示例</kbd>

```
?q=filter(id,gt,0001)-filter(name,lk,Tom).select(id,name,age)
?q=filter(id,gt,0001)+filter(name,lk,Tom).select(id,name,age).order(asc,age,name)
?q=select(id,name,age).filter(id,gt,0005)-filter(name,lk,tom).order(asc,age,name).keys().cut(2,)
```
