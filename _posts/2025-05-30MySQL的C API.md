# MySQL的C API

### 使用C作为mysql的客户端

![image-20250708215500507](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250708215500507.png)

![image-20250709140741823](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250709140741823.png)

### 建立和连接

- **mysql_init()线程不安全，使用init前后记得加锁**

![image-20250709141035127](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250709141035127.png)

#### MySQL连接到线程池

![image-20250709141908884](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250709141908884.png)





![image-20250709143228075](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250709143228075.png)

![image-20250709143156601](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250709143156601.png)

#### 使用字符串存储SQL语句

![image-20250709144133530](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250709144133530.png)

#### mysql_query执行sql语句

![image-20250709144441037](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250709144441037.png)

#### 读类型的语句

- 使用select/show/desc ，mysql_query后必须使用mysql_store_result()
- 

![image-20250709145848740](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250709145848740.png)

![image-20250709145624144](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250709145624144.png)