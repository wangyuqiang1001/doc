### spring事务

#### 一：spring事务嵌套调用

所谓的spring事务嵌套调用指的是发生的不同类的之间的，比如A.methodA()里面调用了B.methodB()方法，通过自身调用方式调用，只会和调用者的事务传播级别有关:在本类中由于通过this调用，不是动态代理对象，导致事务失败，因为事务是基于aop代理对象实现的增强

1. 情况一 

![1587714217479](C:\Users\joymeter\AppData\Roaming\Typora\typora-user-images\1587714217479.png)

数据库db实际情况:

![img](C:\Users\joymeter\AppData\Local\Temp\企业微信截图_15877142484716.png)

均插入失败

2. 情况二 如果testSon()方法，没有事务注解:

![img](C:\Users\joymeter\AppData\Local\Temp\企业微信截图_15877145014958.png)

一样，更加证明testSon()注解失效

3. 把testSon方法，注释。然后实际事务失效，插入进去了:

   ![img](C:\Users\joymeter\AppData\Local\Temp\企业微信截图_15877146653453.png)

两条都成功了,

![img](C:\Users\joymeter\AppData\Local\Temp\企业微信截图_15877146971830.png)

实际上这三种情况的代码相当于:

![img](C:\Users\joymeter\AppData\Local\Temp\企业微信截图_15877147971799.png)

