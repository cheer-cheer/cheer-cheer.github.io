---
layout: post
title:  "Excel：将 'snake_case' 转成 'PascalCase' 或 'camelCase'"
date:   2018-03-19 23:34:05 +0800
categories: Excel
---

如何在 Excel 中将形如 'delivery_id' 的字段变成 PascalCase 形式的 'DeliveryId' 或者 camelCase 的 'deliveryId' 呢？这是在我为 MyBatis Generator 创建配置文件时产生的一个想法。按照规范，数据库中的字段名是 snake_case 形式的，而 Java 中字段名称应该是 camelCase 形式的，那么应该要有一个简单的公式，将 snake_case 直接转为 camelCase（或者 PascalCase）（对，就是懒 Orz）。

tl;dr （太长不看）版:

```
=LOWER(LEFT(SUBSTITUTE(PROPER(A2), "_", ""), 1)) & RIGHT(SUBSTITUTE(PROPER(A2), "_", ""), LEN(SUBSTITUTE(PROPER(A2), "_", "")) - 1)
```
【假设 A2 是数据库字段值】

-----

**公式解析：**

1. 从数据库里读取 `tb_sample` 的表结构：

```sql
desc tb_sample;
```

2. 将列名复制到 Excel 的 A 列：

![columns names](/assets/images/2019-03-19/column_names.png)

3. B 列使用 `PROPER` 函数，将英文单词里首字母变成大写。

```
PROPER(A2)
```

![PROPER columns names](/assets/images/2019-03-19/proper_column_names.png)

4. C 列使用 `SUBSTITUTE` 函数，删掉掉 B 列的 `_` 字符。这就是 PascalCase 了。

```
=SUBSTITUTE(B2, "_", "")
```

![SUBSTITUDE PROPER columns names](/assets/images/2019-03-19/substitude_proper_column_names.png)

5. 如果需要变为 camelCase，只需要对 C 列，多做一个转换，将字符串首字母变为小写，即可：

```
=LOWER(LEFT(C2, 1)) & RIGHT(C2, LEN(C2) - 1)
```

![camelCase columns names](/assets/images/2019-03-19/camel_column_names.png)


所以最终的公式可以写为：

```
=LOWER(LEFT(SUBSTITUTE(PROPER(A2), "_", ""), 1)) & RIGHT(SUBSTITUTE(PROPER(A2), "_", ""), LEN(SUBSTITUTE(PROPER(A2), "_", "")) - 1)
```
