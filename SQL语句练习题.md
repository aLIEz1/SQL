# SQL语句练习题

## 一、用到的表

- 学生表

| 学号 | 姓名 | 性别 | 年龄 | 班级 |
| :--: | :--: | :--: | :--: | :--: |
|      |      |      |      |      |

- 已交作业学生表

| 学号 |
| :--: |
|      |



- 课程表

| 课程号 | 课程名 | 学分 |
| :----: | :----: | :--: |
|        |        |      |



- 成绩表

| 学号 | 课程号 | 成绩 |
| :--: | :----: | :--: |
|      |        |      |

## 二、SQL语句

### 1.查学生表中的所有学生
```sql
SELECT * FROM Student;
```

### 2.查学生表中学生的学号和姓名

```sql
SELECT Sno,Sname FROM Student;
```

### 3.查学生表中的男生

```sql
SELECT * FROM Student WHERE Ssex="男";
```

### 4.查学生表中的女生的学号和姓名
```sql
SELECT Sno,Sname FROM Student WHERE Ssex="女";
```

### 5.查询学生表中性别为男并且年龄大于等于19岁的学生

```sql
SELECT * FROM Student WHERE Ssex="男" AND Sage>=19;
```

### 6.查询学生表中性别为男或者年龄大于等于19岁的学生

```sql
SELECT * FROM Student WHERE Ssex="男" OR Sage>=19;
```

### 7.查询学生表中所有学生，要求按照年龄升序（降序）排序

```sql
SELECT * FROM Student ORDER BY Sage ASC; /*升序*/
SELECT * FROM Student ORDER BY Sage DESC; /*降序*/
```

### 8.查询学生表中所有学生，要求第一按照班级排序，第二按照年龄排序

```sql
SELECT * FROM Student ORDER BY Sclass ASC,Sage ASC; 
```

### 9.查询学生表中性别为男的学生，要求按照班级排序

```sql
SELECT * FROM Student WHERE Ssex="男" ORDER BY Sclass ASC; 
```

### 10.查询学生表中年龄在[19，20]的学生

```sql
SELECT * FROM Student WHERE Sage BETWEEN 19 AND 20;
```

### 11.查询学生表中姓张的学生

```sql
SELECT * FROM Student WHERE Sname LIKE "张%";
```

### 12.查询学生表中姓名含石的学生

```sql
SELECT * FROM Student WHERE Sname LIKE "%石%";
```

### 13.查询学生表中男生的人数

```sql
SELECT COUNT(*) FROM Student WHERE Ssex="男";
```

### 14.查询学生表中年龄最大的学生

```sql
SELECT * FROM Student WHERE Sage > ALL(SELECT Sage FROM Student);
```

### 15.查询学生表中年龄最小的学生

```sql
SELECT * FROM Student WHERE Sage < ALL(SELECT Sage FROM Student);
```

### 16.查询学生中的平均年龄

```sql
SELECT AVG(Sage) FROM Student;
```

### 17.查询学生表中年龄之和

```sql
SELECT SUM(Sage) FROM Student;
```

### 18.查询学生表中男女生的人数各多少人

```sql
SELECT Ssex,COUNT(*) FROM Student GROUP BY Ssex;
```

### 19.查询学生表中各个班的平均年龄

```sql
SELECT Sclass,AVG(Sage) FROM Student GROUP BY Sclass;
```

### 20.查询学生表中各个班级男女生人数

```sql
SELECT Sclass,Ssex,COUNT(*) FROM Student GROUP BY Sclass,Ssex;
```

### 21.查询学生表中学号为1001，1003，1006，1010的学生

```sql
SELECT * FROM Student WHERE Sno IN("1001","1003","1010");
```

### 22.查询未交作业的学生

```sql
SELECT * FROM Student WHERE Sno NOT IN(SELECT Sno FROM Work);
```

### 23.查询学号，姓名，课程号，成绩

```sql
SELECT Student.Sno,Student.Sname,Course.Cno,Course.Grade FROM Student INNER JOIN Course ON Student.Sno=Course.Sno;
```

### 24.将（1022，张望，男，19，信息2）的学生插入到学生表中

```sql
INSERT INTO Student(Sno,Sname,Ssex,Sage,Sclass) VALUES("1022","张望","男","19","信息2");
```

### 25.将学号为1022学生的姓名改为张旺

```sql
UPDATE Student SET Sname="张旺" WHERE Sno="1022";
```

### 26.删除学号为1022的学生

```sql
DELETE FROM Student WHERE Sno="1022";
```

#### 27.将学生表中的数据复制到“学生表备份”中

```sql
INSERT INTO Backup(Sno,Sname,Ssex,Sage,Sclass) SELECT Sno,Sname,Ssex,Sage,Sclass FROM Student;
```

### 28.将学生表中的数据复制到“学生表备份”中（学生备份表不空）

```sql
INSERT INTO Backup(Sno,Sname,Ssex,Sage,Sclass) SELECT Sno,Sname,Ssex,Sage,Sclass FROM Student WHERE Sno NOT IN (SELECT Sno FROM Backup);
```

### 29.将学生表1和学生表2的内容显示出来

```sql
SELECT * FROM Student1 UNION SELECT * FROM Student2;
```