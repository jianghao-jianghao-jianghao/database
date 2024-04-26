1) 从职工关系中检索所有工资
```sql
SELECT 工资 FROM 职工;
```
2)	检索仓库关系中的所有元组
```sql
SELECT * FROM 仓库;
```

4) 检索工资多于1230元的职工号：
```sql
SELECT 职工号 FROM 职工 WHERE 工资 > 1230;
```

4) 找出尚未确定供应商的订购单：
```sql
SELECT 订购单号 FROM 订购单 WHERE 供应商号 IS NULL;
```

5) 检索在北京的供应商的名称：
```sql
SELECT 供应商名 FROM 供应商 WHERE 地址 = '北京';
```

6) 检索发给供应商S6的订购单号：
```sql
SELECT 订购单号 FROM 订购单 WHERE 供应商号 = 'S6';
```

7) 检索出职工E6发给供应商S6的订购单信息：
```sql
SELECT * FROM 订购单 WHERE 职工号 = 'E6' AND 供应商号 = 'S6';
```

8) 检索出在仓库WH1或WH2工作，并且工资少于1250元的职工号：
```sql
SELECT 职工号 FROM 职工 WHERE 仓库号 IN ('WH1', 'WH2') AND 工资 < 1250;
```

9) 检索出向供应商S3发过订购单的职工的职工号和仓库号：
```sql
SELECT DISTINCT 职工.职工号, 职工.仓库号 FROM 职工
JOIN 订购单 ON 职工.职工号 = 订购单.职工号
WHERE 订购单.供应商号 = 'S3';
```

10) 检索出目前与S3供应商没有联系的职工信息：
```sql
SELECT * FROM 职工 WHERE 职工号 NOT IN (
    SELECT 职工号 FROM 订购单 WHERE 供应商号 = 'S3'
);
```

11) 检索出目前和华通电子公司有业务联系的每个职工的工资：
```sql
SELECT 职工.工资 FROM 职工
JOIN 订购单 ON 职工.职工号 = 订购单.职工号
JOIN 供应商 ON 订购单.供应商号 = 供应商.供应商号
WHERE 供应商.供应商名 = '华通电子公司';
```

12) 检索出向S4供应商发出订购单的仓库所在的城市：
```sql
SELECT DISTINCT 仓库.城市 FROM 仓库
JOIN 职工 ON 仓库.仓库号 = 职工.仓库号
JOIN 订购单 ON 职工.职工号 = 订购单.职工号
WHERE 订购单.供应商号 = 'S4';
```

13) 检索出在上海工作并且向S6供应商发出了订购单的职工号：
```sql
SELECT DISTINCT 职工.职工号 FROM 职工
JOIN 仓库 ON 职工.仓库号 = 仓库.仓库号
JOIN 订购单 ON 职工.职工号 = 订购单.职工号
WHERE 仓库.城市 = '上海' AND 订购单.供应商号 = 'S6';
```

14) 检索出由工资多于1230元的职工向北京的供应商发出的订购单号：
```sql
SELECT 订购单.订购单号 FROM 订购单
JOIN 职工 ON 订购单.职工号 = 职工.职工号
JOIN 供应商 ON 订购单.供应商号 = 供应商.供应商号
WHERE 职工.工资 > 1230 AND 供应商.地址 = '北京';
```

15) 检索出仓库的个数：
```sql
SELECT COUNT(*) FROM 仓库;
```

16) 检索出有最大面积的仓库信息：
```sql
SELECT * FROM 仓库 WHERE 面积 = (SELECT MAX(面积) FROM 仓库);
```

17) 检索出所有仓库的平均面积：
```sql
SELECT AVG(面积) FROM 仓库;
```

18) 检索出向S4供应商发出订购单的那些仓库的平均面积：
```sql
SELECT AVG(仓库.面积) FROM 仓库
JOIN 职工 ON 仓库.仓库号 = 职工.仓库号
JOIN 订购单 ON 职工.职工号 = 订购单.职工号
WHERE 订购单.供应商号 = 'S4';
```

19) 检索出每个城市的供应商个数：
```sql
SELECT 地址 AS 城市, COUNT(*) AS 供应商个数 FROM 供应商
GROUP BY 地址;
```

20) 检索出每个仓库中工资多于1220元的职工个数：
```sql
SELECT 仓库号, COUNT(*) AS 职工个数 FROM 职工
WHERE 工资 > 1220
GROUP BY 仓库号;
```

21) 检索出和面积最小的仓库有联系的供应商的个数：
```sql
SELECT COUNT(DISTINCT 供应商号) FROM 订购单
WHERE 职工号 IN (
    SELECT 职工号 FROM 职工 WHERE 仓库号 = (
        SELECT 仓库号 FROM 仓库 WHERE 面积 = (SELECT MIN(面积) FROM 仓库)
    )
);
```
