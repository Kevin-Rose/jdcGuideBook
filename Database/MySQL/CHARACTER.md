##### d处理数据库之间编码不一致

+ 修改表的编码
     ```
  ALTER TABLE chat_comments_meituan DEFAULT CHARACTER 
  SET utf8mb4 COLLATE=utf8mb4_general_ci;
  ```
  
+ 修改表字段的编码
  ```
  ALTER TABLE chat_comments_meituan CONVERT TO CHARACTER
  SET utf8mb4 COLLATE utf8mb4_general_ci;
  ```