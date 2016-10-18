title: 使用Hibernate执行sql结果转换bean
date: 2016-10-18 18:03:25
categories:
- 学习
tags:
- Java
---

在使用Hibernate的时候，不可避免要执行一些比较复杂的sql语句，在这备忘一些执行的结果集转成bean的方法。
<!--more-->

## 假如有一个bean，不一定要是hibernate映射的bean
```java
public class User {
	private String name;
	private String sex;
	private String phone;
	private int age;

	........ get set
}
```

## Hibernate查询方法
```java
	@Override
	@Transactional(readOnly = true)
	public List<User> getUser(String username, String age) {
		String sql = "select name, sex, phone, age from t_user where name = :name and age = :age";

		Session session = sessionFactory.getCurrentSession();
        SQLQuery query = session.createSQLQuery(sql);
        query.setResultTransformer(Transformers.aliasToBean(User.class));
        query.addScalar("name").addScalar("sex").addScalar("phone").addScalar("age", IntegerType.INSTANCE);
        query.setString("name", name);
        query.setString("age", age);

		return query.list();
	}
```
addScalar方法必须要设置，假如字段不是字符串的时候要设置类型。



转发表明出处，谢谢！