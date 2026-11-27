---
layout: post
title: "MySQL GROUP_CONCAT函数使用示例：如何用一个SQL查询出一个班级各个学科第N名是谁？"
date: 2016-06-16 10:40:00 +0800
categories: mysql sql
---

如何用一个SQL查询出一个班级各个学科第N名是谁？

首先贴出建表语句，方便大家本地测试：

```
-- 建表语句
CREATE TABLE score (
    id INT NOT NULL auto_increment,
    `name` VARCHAR (20) NOT NULL DEFAULT '' COMMENT '姓名',
    sub VARCHAR (20) NOT NULL DEFAULT '' COMMENT '学科',
    score INT NOT NULL DEFAULT 0 COMMENT '分数',
    PRIMARY KEY (id)
);
 
INSERT INTO `score` (`id`, `name`, `sub`, `score`) VALUES ('1', '麻子', '语文', '85');
INSERT INTO `score` (`id`, `name`, `sub`, `score`) VALUES ('2', '王二', '语文', '99');
INSERT INTO `score` (`id`, `name`, `sub`, `score`) VALUES ('3', '张三', '语文', '76');
INSERT INTO `score` (`id`, `name`, `sub`, `score`) VALUES ('4', '李四', '语文', '96');
INSERT INTO `score` (`id`, `name`, `sub`, `score`) VALUES ('5', '学霸', '语文', '100');
INSERT INTO `score` (`id`, `name`, `sub`, `score`) VALUES ('6', '麻子', '数学', '66');
INSERT INTO `score` (`id`, `name`, `sub`, `score`) VALUES ('7', '王二', '数学', '88');
INSERT INTO `score` (`id`, `name`, `sub`, `score`) VALUES ('8', '张三', '数学', '99');
INSERT INTO `score` (`id`, `name`, `sub`, `score`) VALUES ('9', '李四', '数学', '33');
INSERT INTO `score` (`id`, `name`, `sub`, `score`) VALUES ('10', '学霸', '数学', '100');
INSERT INTO `score` (`id`, `name`, `sub`, `score`) VALUES ('11', '麻子', '英语', '98');
INSERT INTO `score` (`id`, `name`, `sub`, `score`) VALUES ('12', '王二', '英语', '99');
INSERT INTO `score` (`id`, `name`, `sub`, `score`) VALUES ('13', '张三', '英语', '60');
INSERT INTO `score` (`id`, `name`, `sub`, `score`) VALUES ('14', '李四', '英语', '59');
INSERT INTO `score` (`id`, `name`, `sub`, `score`) VALUES ('15', '学霸', '英语', '100');
```

我自己想出的一个sql方案，用到了GROUP\_CONCAT和SUBSTRIlNG\_INDEX两个函数：

```
-- SQL
SET @rank = 3;
SELECT
    s.sub,
    s.`name`,
    s.score
FROM
    (
        SELECT
            sub,
            SUBSTRING_INDEX(
                SUBSTRING_INDEX(
                    GROUP_CONCAT(score ORDER BY score DESC),
                    ',',
                    @rank
                ),
                ',' ,- 1
            ) AS score
        FROM
            score
        GROUP BY
            sub
    ) AS t
LEFT JOIN score AS s ON (
    s.sub = t.sub
    AND s.score = t.score
```

GROUP\_CONCAT的官方解释：

This function returns a string result with the concatenated non-`NULL` values from a group. It returns `NULL` if there are no non-`NULL` values. The full syntax is as follows:

```
GROUP_CONCAT([DISTINCT] expr [,expr ...]
             [ORDER BY {unsigned_integer | col_name | expr}
                 [ASC | DESC] [,col_name ...]]
             [SEPARATOR str_val])
```

In MySQL, you can get the concatenated values of expression combinations. To eliminate duplicate values, use the DISTINCT clause. To sort values in the result, use the ORDER BY clause. To sort in reverse order, add the DESC (descending) keyword to the name of the column you are sorting by in the ORDER BY clause. The default is ascending order; this may be specified explicitly using the ASC keyword. The default separator between values in a group is comma (“,”). To specify a separator explicitly, use SEPARATOR followed by the string literal value that should be inserted between group values. To eliminate the separator altogether, specify SEPARATOR ''.

有其他方法的，大家可以一起讨论。
