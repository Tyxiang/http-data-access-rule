# Query the OVL result

## 1. Query method

### 1.1. filter

📌 Format

```
filter({key},{cmpr},{value})
```

📌 Description

- `cmpr` Comparison symbol:

| Symbol | Semantic              |
| ------ | --------------------- |
| `eq`   | equal                 |
| `ne`   | not equal to          |
| `gt`   | more than the         |
| `lt`   | less than             |
| `ge`   | greater or equal to   |
| `le`   | less than or equal to |
| `lk`   | like                  |

- Multiple filters can be used in combination:

| Symbol | Semantic        |
| :----: | --------------- |
|  `+`   | set merge       |
|  `-`   | set subtraction |

📌 Example

```
?q=filter(id,eq,'0001')   // Filter out items with id equal to '0001'
?q=filter(age,ge,20)      // Filter out items that age is greater than or equal to 20
?q=filter(name,lk,'tom')  // Filter out items that name is similar to tom
?q=filter(id,gt,0005)-filter(name,lk,Tom)
?q=filter(age,gt,15)+filter(name,lk,Tom)
```

### 1.4. Order

📌 Format

```
order({way},{key1})
order({way},{key1},{key2})
order({way},{key1},{key2},{key3},...)
```

📌 Description

- There are two options for `way`, `asc` from small to large, and `des` from large to small.
- When sorting, the key on the left takes precedence;

📌 Example

```
?q=order(asc,name,age)    // Sort from smallest to largest, name first, age second
```

### 1.5. Select Column

📌 Format

```
select({key})
select({key1},{key2})
select({key1},{key2},{key3},...)
```

📌 Example

```
?q=select(name,age)  // Select the name and age columns
```

### 1.6. Get Keys

📌 Format

```
keys()
```

📌 Description

- Return all keys.

📌 Example

```
?q=keys()
```

### 1.7. Get Value

📌 Format

```
values()
```

📌 Description

- Return all values.

📌 Example

```
?q=values()
```

### 1.8. Cut

📌 Format

```
cut({start},{end})
cut({start})
cut({start},)
cut(,{end})
cut(,)
```

📌 Description

- `start` The starting index.
- `end` The ending index. 
- The index can be negative.

📌 Example

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

## 2. Combination of query methods

📌 Description

- The query methods can be used in combination, the combinator is `.`.
- The combination is processed from left to right, the output on the left is the input on the right.

📌 Example

```
?q=filter(id,gt,0001)-filter(name,lk,Tom).select(id,name,age)
?q=filter(id,gt,0001)+filter(name,lk,Tom).select(id,name,age).order(asc,age,name)
?q=select(id,name,age).filter(id,gt,0005)-filter(name,lk,tom).order(asc,age,name).keys().cut(2,)
```
