# Statistic on the OVL result

📌 Format

| Method  | Format       | Description                        | Example       |
| ------- | ------------ | ---------------------------------- | ------------- |
| maximum | `max({key})` | Return the largest item            | `?s=max(age)` |
| minimum | `min({key})` | Return the smallest item           | `?s=min(age)` |
| average | `avg({key})` | Return the average                 | `?s=avg(age)` |
| count   | `count()`    | Return the total number of members | `?s=count()`  |

📌 Description

- Take statistic on the result and return the statistical result.

📌 Example

The following example has the same result:

```
?s=max(age)
?s=count()
```
