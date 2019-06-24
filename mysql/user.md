# MYSQL 데이터베이스 User 추가하기

MYSQL 데이터베이스 User 추가하기

## Create database

```bash
CREATE DATABASE database;
```

## Create user

```bash
CREATE USER 'userID'@'localhost' IDENTIFIED BY 'userPassword';
```

## Grant

```bash
GRANT DELETE, INSERT, SELECT, UPDATE ON database.* TO `user`@`host`;
```
