# 组合使用

| 查询组合符 | 语义 | 说明                                   |
| :--------: | :--: | -------------------------------------- |
|    `+`     |  与  | 从左到右处理，左侧的输出是右侧的输入； |
|    `,`     |  或  |                                        |

```
?q=filter(id,gt,0001)+search(name,Tom)&s=max()
?q=filter(id,gt,0001),search(name,Tom,Jarry)+select(id,name,age)&s=count()
?q=filter(id,gt,0001)+search(name,Tom)+select(id,name,age)+except(age,20)
?q=filter(id,gt,0001),search(name,Tom,Jarry)+select(id,name,age)+except(age,20)
?q=except(name,Tom)+except(from,beijing)    // 去除 name 为 Tom 或 from 为 beijing 的项
?q=except(name,Tom),except(from,beijing)    // 去除 name 为 Tom 且 from 为 beijing 的项
?q=search(name,Tom)+search(from,beijing)    // 搜索 name 为 Tom 且 from 为 beijing 的项
?q=search(name,Tom),search(from,beijing)    // 搜索 name 为 Tom 或 from 为 beijing 的项
```
