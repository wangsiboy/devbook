## 插入数据

为主键列打开自增（auto-increment）特性。介绍下另一种SQL方案语句-alter table，它用于修改已存在的表定义：

```
ALTER TABLE persion MODIFY person_id SMALLINT UNSIGNED AUTO_INCREMENT;
```

* **insert语句**

```
/* 添加个叫William Turner的家伙 */
INSERT INTO person 
(person_id, name, gender, birth_date)
VALUES (null, 'William Turner', 'M', '1972-05-27');

/* 查询下 */
SELECT person_id, name, birth_date 
FROM person
WHERE person_id=1;


```

```
INSERT INTO favorite_food 
 (person_id, food)
 VALUES (1, 'pizza');

INSERT INTO favorite_food
 (person_id, food)
 VALUES (1, 'cookies');
 
SELECT food
FROM favorite_food
WHERE person_id=1
ORDER BY food;
```

order by 子句指示对查询返回进行排序。不使用次序不做任何保证。

> 获取XML格式的数据
>
> mysql -u mlgm -p --xml bank

## 更新数据

```
/* 给William Turner添加地址信息 */
UPDATE person
SET street = '1225 Tremont St.',
  city = 'Boston',
  state = 'MA',
  country = 'USA',
  postal_code = '02138'
WHERE person_id = 1;
```

## 删除数据

```
DELETE FROM person;
/* 没有where子句，表中的所有行都会被删除 */
```



