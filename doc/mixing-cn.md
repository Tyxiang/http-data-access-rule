# 混合使用

<kbd>说明</kbd>

- 用 `&` 实现查询与统计的组合；
- 查询会被先执行；
- 统计会被后执行；
- 查询的输出会被作为统计的输入；

<kbd>示例</kbd>

```  
?q=filter(age,gt,18)&s=max(age)
?q=s=max(age)&filter(age,gt,18) 
```
注：以上示例的结果相同。