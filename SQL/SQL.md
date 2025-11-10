# SQL笔记

## CHECK约束的添加与删除
	添加CHECK约束：ALTER TABLE 表名 ADD CONSTRAINT 约束名 (条件表达式)
	例如：ALTER TABLE course ADD CONSTRAINT check_ccredit CHECK ((Ccredit > 0) && (Ccredit < 10))
	删除CHECK约束：ALTER TABLE 表名 DROP CONSTRAINT 约束名
	例如：ALTER TABLE course DROP CONSTRAINT check_ccredit

## 主码的添加与删除
	添加主码：ALTER TABLE 表名 ADD CONSTRAINT 约束名 PRIMARY KEY(列1，列2)
	例如：
	删除主码：ALTER TABLE 表名 DROP PRIMARY KEY
	例如：

## 外码的添加与删除
	添加外码：ALTER TABLE 表名 ADD CONSTRAINT 约束名 外码约束
	例如：
	删除外码：ALTER TABLE 表名 DROP CONSTRAINT 约束名
	例如：ALTER TABLE course DROP CONSTRAINT Tid 

## 创建唯一约束
	ALTER TABLE 表名 ADD CONSTRAINT 约束名 UNIQUE (列名)
	例如：ALTER TABLE teacher ADD CONSTRAINT unique_email UNIQUE (Temail)

## 多表连接和条件查询
	SELECT 
		student.Sname, course.Cname, sc.Score, teacher.Tname 
	FROM 
		sc 
	JOIN 
		student ON sc .Sid = student .Sid 
	JOIN 
		course ON sc.Cid = course .Cid 
	JOIN
		teacher ON course.Tid = teacher.Tid 
	WHERE 
		teacher.Tgender = '女' AND
		course.Ccredit >= 3 AND
		sc.Score >= 90
	
## 建立索引
	CREATE INDEX id_22373400 ON teacher(Tid);

## 建立视图
	CREATE VIEW SC_22 AS
	SELECT 
		sc .Sid ,
		sc .Cid ,
		sc .Score
	FROM 
		sc 
	JOIN 
		student ON sc.Sid  = student .Sid 
	WHERE 
		SUBSTRING(CAST(sc.Sid AS CHAR), 1, 2) = '22';

## 将编号最大的两门课程的类型改为必修
	WITH RankedCourses AS (  
		SELECT  
			Cid,  
			ROW_NUMBER() OVER (ORDER BY Cid DESC) AS rn  
		FROM  
			course  
	)  
	UPDATE course  
	INNER JOIN RankedCourses ON course.Cid = RankedCourses.Cid  
	SET course.Ctype = '必修'  
	WHERE RankedCourses.rn <= 2;

## 将Y老师的教授的所有课的学生的成绩更改为Z分
	# score中只有Sid, Cid和Score，所以需要根据Cid找相应的课程，然后再找对应的老师
	UPDATE sc 
	SET Score = 100
	WHERE Cid  IN (  
		SELECT Cid   
		FROM course
		JOIN teacher ON course.Tid = teacher.Tid 
		WHERE teacher.Tname = '万寒'
	);

