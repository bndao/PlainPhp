# PlainPhp App

Just some php.

## Setup

Be careful not to have important things is the news database before playing this !!!!!!

``` sql
CREATE USER 'news'@'localhost' IDENTIFIED BY 'newspass';

DROP DATABASE if exists news;
CREATE DATABASE news;
USE news;

CREATE TABLE `news` (
  `id` bigint(20) unsigned NOT NULL auto_increment,
  `author` varchar(30) NOT NULL,
  `title` varchar(100) NOT NULL,
  `content` text NOT NULL,
  `dateAdded` datetime NOT NULL,
  `dateModif` datetime NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `title` (`title`),
  KEY (`author`, `title`)
) DEFAULT CHARSET=utf8;
CREATE TABLE `users` (
  `id` bigint(20) unsigned NOT NULL auto_increment,
  `nickname` varchar(30) NOT NULL,
  `email` varchar(70) default NULL,
  `password` varchar(256) default NULL,
  `accessLevel` tinyint(3) unsigned NOT NULL default '0',
  `creationDate` datetime NOT NULL,
  `lastAccess` datetime NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `email` (`email`),
  UNIQUE KEY `nickname` (`nickname`),
  KEY (`email`, `nickname`)
) DEFAULT CHARSET=utf8;

INSERT INTO users SET nickname='defaultNickName', email='defaultEmail@email.com', password='pwd', accessLevel='1', creationDate=NOW(), lastAccess=NOW();

GRANT ALL PRIVILEGES on news.* to 'news'@'localhost' IDENTIFIED BY 'newspass';
FLUSH PRIVILEGES;
SHOW GRANTS FOR 'news'@'localhost';

```

## Run

```bash
php -S localhost:8080 -t Public
```
Then visit `http://localhost:8080` that's it...
