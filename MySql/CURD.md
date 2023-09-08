# CURD



## SELECT

通用查询模板

```sql
SELECT ......., .......
FROM ...
[(LEFT / RIGHT) JOIN ... ON ... = ...]
GROUP BY ...
HAVING ...(聚合函数)
ORDER ... BY ... (ASC / DESC) [ ,... (ASC / DESC)]
LIMIT ...(index, PageSize)
```

- index：起始索引
- PageSize：每页条数
- index = (PageNum - 1) * PageSize



### 多表查询

内连接

```sql
SELECT ......., .......
FROM ...
INNER JOIN ... ON ... = ...
```

左外连接

```sql
SELECT ......., .......
FROM ...
LEFT OUTER JOIN ... ON ... = ...
```

右外连接

```sql
SELECT ......., .......
FROM ...
RIGHT OUTER JOIN ... ON ... = ...
```

满外连接

```sql
# Oracle用
SELECT ......., .......
FROM ...
FULL OUTER JOIN ... ON ... = ...

# MySql 用
UNION          # 去重
UNION ALL      # 不去重
```



## 插入

```shell
INSERT INTO tableName VALUES();
```



## 改

```shell
UPDATE tableName SET ... WHERE ...
```



## 删除

```shell
DELETE FROM tableName WHERE ...
```

