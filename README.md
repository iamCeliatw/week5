# week5 Assignment 

### 要求三：SQL CRUD

**1.使用 INSERT 指令新增一筆資料到 member 資料表中，這筆資料的 username 和 password 欄位必須是 test。接著繼續新增至少 4 筆隨意的資料**
```sql
INSERT INTO `member` (`name`,`username`,`follower_count`, 
`password`)VALUES('測試用''test',10,'test');
INSERT INTO `member` (`name`,`username`,`follower_count`, `password`)VALUES('第二筆','two',56,'two');
INSERT INTO `member` (`name`,`username`,`follower_count`, `password`)VALUES('第三筆','three',77,'three');
INSERT INTO `member` (`name`,`username`,`follower_count`, `password`)VALUES('第四筆','four',181,'four');
INSERT INTO `member` (`name`,`username`,`follower_count`, `password`)VALUES('第五筆','five',223,'five');
```

![](https://i.imgur.com/GB9fROe.png)

**2.使用 SELECT 指令取得所有在 member 資料表中的會員資料。**
```sql
SELECT * FROM `member`;
```
![](https://i.imgur.com/CNPksPF.png)

**3.使用 SELECT 指令取得所有在 member 資料表中的會員資料，並按照 time 欄位，由近到遠排序。**
```sql
SELECT * FROM `member` ORDER BY `time` DESC;
```
![](https://i.imgur.com/cV2IaDc.png)


**4.使用 SELECT 指令取得 member 資料表中第 2 ~ 4 共三筆資料，並按照 time 欄位，由近到遠排序。( 並非編號 2、3、4 的資料，而是排序後的第 2 ~ 4 筆資料 )**
```sql
SELECT * FROM `member` ORDER BY `time` DESC LIMIT 1,3;
```

![](https://i.imgur.com/L1jJVCi.png)

**5.使用 SELECT 指令取得欄位 username 是 test 的會員資料。**
```sql
SELECT *
FROM `member`
WHERE `password` LIKE 'test' ;
```

![](https://i.imgur.com/xwbf7Sh.png)

**6.使用 SELECT 指令取得欄位 username 是 test、且欄位 password 也是 test 的資料。**

```sql
SELECT *
FROM `member`
WHERE `password` LIKE 'test' AND `username` LIKE 'test';
```
![](https://i.imgur.com/g691QTe.png)

**7.使用 UPDATE 指令更新欄位 username 是 test 的會員資料，將資料中的 name 欄位改成 test2。**
```sql
UPDATE `member` 
SET `name`='test2'
WHERE `username`='test'; 
SELECT * FROM `member` WHERE `username`='test';
```
![](https://i.imgur.com/1Flb0XU.png)

![](https://i.imgur.com/6oab4lT.png)

### 要求四:SQL Aggregate Functions

**1. 取得 member 資料表中，總共有幾筆資料 ( 幾位會員 )。**
```sql!
SELECT COUNT(*) FROM `member`;
```

![](https://i.imgur.com/MxaaKhK.png)





**2. 取得 member 資料表中，所有會員 follower_count 欄位的總和。**
```sql
SELECT SUM(`follower_count`) FROM `member`;
```
![](https://i.imgur.com/6wn7huV.png)

**3. 取得 member 資料表中，所有會員 follower_count 欄位的平均數。**
```sql
 SELECT round(AVG(follower_count),1) FROM `member`;
 ```

![](https://i.imgur.com/FXQqNnZ.png)



### 要求五：SQL JOIN (Optional)

**1.在資料庫中，建立新資料表紀錄留言資訊，取名字為 message。資料表中必須包含以下欄位設定**

```sql 
CREATE TABLE `message` (
    `id` BIGINT PRIMARY KEY AUTO_INCREMENT,
    `member_id` BIGINT NOT NULL,
    `content` VARCHAR(255) NOT NULL,
    `like_count` INT UNSIGNED NOT NULL DEFAULT 0,
    `time` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP()
);

ALTER TABLE `message`
    ADD FOREIGN KEY (`member_id`)
    REFERENCES `member`(`id`);
```
![](https://i.imgur.com/oKVI2hk.png)

```sql
SELECT * FROM `message`;
```
![](https://i.imgur.com/1tsqEUv.png)


**2.使用 SELECT 搭配 JOIN 語法，取得所有留言，結果須包含留言者會員的姓名。**

```sql!
SELECT `content`,`name`
FROM `message`
LEFT JOIN `member`
ON message.member_id = `member.id`;
```
![](https://i.imgur.com/wrtcZBl.png)


**3.使用 SELECT 搭配 JOIN 語法，取得 member 資料表中欄位 username 是 test 的所有留言，資料中須包含留言者會員的姓名。**

```sql!
SELECT `name`,`content`
FROM `message`
RIGHT JOIN `member`
ON (message.member_id = member.id)
WHERE (member.username = 'test');
```

![](https://i.imgur.com/NkxeX3Q.png)


**4.使用 SELECT、SQL Aggregate Functions 搭配 JOIN 語法，取得 member 資料表中
欄位 username 是 test 的所有留言平均按讚數。**

```sql!
SELECT round(AVG(like_count),2)
FROM `message`
JOIN `member`
ON (message.member_id = member.id)
WHERE (member.username = 'test');
```

![](https://i.imgur.com/xKz2ZiS.png)

