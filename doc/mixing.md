# Mix using

<kbd>📌 Description</kbd>

- You can use `&` to combine query and statistic.
- The query will be executed first.
- The statistic will be executed later.
- The output of the query will be used as the input of the statistic.

<kbd>📌 Example</kbd>

```  
?q=filter(age,gt,18)&s=max(age)
?q=s=max(age)&filter(age,gt,18) 
```
Note: The results of the above examples are the same. 