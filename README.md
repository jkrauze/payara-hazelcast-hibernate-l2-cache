# Hibernate on Payara Micro with L2 cache enabled

*This repository is based on [hibernate-example](https://github.com/payara/Payara-Examples/tree/master/javaee/hibernate-example) Payara Micro official examples.*


Steps to reproduce problem:

1. Clone or download this repository.
1. Build and run Payara Micro Uber-jar using Payara Micro Maven Plugin
```
mvn clean package payara-micro:bundle payara-micro:start
```

One can easily check if L2 cache is working by adding an entity (`POST /resources/person`) and then fetching it by ID (`GET /resources/person/{id}`). If L2 cache is working, you will see only
```
Hibernate: call next value for hibernate_sequence
Hibernate: insert into Person (lastName, name, id) values (?, ?, ?)
```
in console.
If L2 cache is not working, you will also see the SELECT statement on each GET request.
```
Hibernate: select person0_.id as id1_0_0_, person0_.lastName as lastName2_0_0_, person0_.name as name3_0_0_ from Person person0_ where person0_.id=?
```
