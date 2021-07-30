# OVL 结果集的统计 Statistic

## 1. 方法

### 1.1. 数量

<kbd>格式</kbd>

```
count()
```

<kbd>示例</kbd>

```
?s=count()
```

### 1.2. 最大

<kbd>格式</kbd>

```
max({key})
```

<kbd>示例</kbd>

```
?s=max(age)
```

### 1.3. 最小

<kbd>格式</kbd>

```
min({key})
```

<kbd>示例</kbd>

```
?s=min(age)
```

### 1.4. 平均

<kbd>格式</kbd>

```
avg({key})
```

<kbd>示例</kbd>

```
?s=avg(age)
```

## 2. 组合

<kbd>示例</kbd>

```
?q=filter(id,gt,0001)+search(name,Tom)&s=max()
?q=filter(id,gt,0001),search(name,Tom,Jarry)+select(id,name,age)&s=count()
```
