# coursework
Very Simple Renting Platform

[安装部署](https://github.com/rao1219/olhandicrafts/wiki/install)

----
## 前端
库用的bootstrap和jQuery，前端状态如下：


```flow
				
						   	      +----------------+	
						      +--->crafts require  <-----------------------------+
		                      |   +----------------+							 |
						      | 											     |
						      |	  +----------------+		                     | 
						      +--->crafts overview |	   +---------------+     |
						      |   +----------------+  +---->publish needs  +--(json)
	+-------+                 |						  |	   +---------------+    
	|       |    			  |                       |
	| index |  			      |   +---------------+   |	   +---------------+
	|       +--(login/regist)-+--->user management+---+----> profile	   |
	+-------+  	 		      |   +---------------+   |	   +---------------+
						      |                       |	
						      |						  |    +--------------+
						      |                       +----> my orders    |
						      |   +---------------+		   +--------------+
						      +--->product detail |
						 	      +---------------+

```		
+ 此图只表明网页/状态之间的相关关系，并不能描述所有的路由和跳转规则。
+ 试图将不同网页公用模板表示在一起。例如用户信息管理如果是可修改状态则可用于修改当前用户资料，否则用于显示他人资料。



## 后端
使用php自行开发，为MVC框架
提供

+ 用户管理  
+ 订单管理  
+ 需求管理  
+ Session management   


### 数据库
+ ER 图
![er model](https://github.com/rao1219/olhandicrafts/blob/master/style/images/er-model.png)



+ SQL：
```sql

-- MySQL Script generated by MySQL Workbench
-- 12/01/15 16:12:22
-- Model: New Model    Version: 1.0
-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='TRADITIONAL,ALLOW_INVALID_DATES';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
-- -----------------------------------------------------
-- Schema handicrafts
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema handicrafts
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `handicrafts` DEFAULT CHARACTER SET latin1 ;
USE `handicrafts` ;

-- -----------------------------------------------------
-- Table `handicrafts`.`admin`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `handicrafts`.`admin` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `user` VARCHAR(32) NULL DEFAULT NULL,
  `password` VARCHAR(32) NULL DEFAULT NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `handicrafts`.`city`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `handicrafts`.`city` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `city` VARCHAR(30) NOT NULL,
  `parentid` INT(11) NOT NULL DEFAULT '0',
  `layer` TINYINT(4) NOT NULL DEFAULT '1',
  `sort` TINYINT(4) NOT NULL DEFAULT '1',
  PRIMARY KEY (`id`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `handicrafts`.`communicate`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `handicrafts`.`communicate` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `userid` INT(11) NOT NULL,
  `time` VARCHAR(20) NOT NULL DEFAULT '0',
  `content` TEXT NULL DEFAULT NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `handicrafts`.`sort`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `handicrafts`.`sort` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(20) NOT NULL DEFAULT '0',
  PRIMARY KEY (`id`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `handicrafts`.`crafts`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `handicrafts`.`crafts` (
  `id` INT(11) NOT NULL,
  `name` VARCHAR(45) NULL DEFAULT NULL,
  `type` VARCHAR(45) NULL DEFAULT NULL,
  `price` INT(11) NULL DEFAULT NULL,
  `color` VARCHAR(45) NULL DEFAULT NULL,
  `seller` VARCHAR(45) NULL DEFAULT NULL,
  `selleradd` VARCHAR(45) NULL DEFAULT NULL,
  `phone` VARCHAR(45) NULL DEFAULT NULL,
  `title` VARCHAR(45) NULL DEFAULT NULL,
  `store` VARCHAR(45) NULL DEFAULT NULL,
  `description` VARCHAR(45) NULL DEFAULT NULL,
  `img` VARCHAR(45) NULL DEFAULT NULL,
  PRIMARY KEY (`id`),
  CONSTRAINT `fk_crafts_sort1`
    FOREIGN KEY (`id`)
    REFERENCES `handicrafts`.`sort` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `handicrafts`.`order`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `handicrafts`.`order` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `productName` VARCHAR(20) NOT NULL,
  `price` INT(11) NOT NULL,
  `number` INT(11) NOT NULL,
  `state` TINYINT(4) NOT NULL DEFAULT '0',
  `buyername` VARCHAR(20) NULL DEFAULT NULL,
  `buyerphone` VARCHAR(20) NULL DEFAULT NULL,
  `buyeraddress` VARCHAR(30) NULL DEFAULT NULL,
  `sellername` VARCHAR(20) NULL DEFAULT NULL,
  `sellerphone` VARCHAR(20) NULL DEFAULT NULL,
  `selleraddress` VARCHAR(30) NULL DEFAULT NULL,
  `comments` TEXT NULL DEFAULT NULL,
  `time1` VARCHAR(20) NOT NULL DEFAULT '0',
  `time2` VARCHAR(20) NOT NULL DEFAULT '0',
  `time3` VARCHAR(20) NOT NULL DEFAULT '0',
  `time4` VARCHAR(20) NOT NULL DEFAULT '0',
  `bcomment` TEXT NULL DEFAULT NULL,
  `somment` TEXT NULL DEFAULT NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `handicrafts`.`member`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `handicrafts`.`member` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `username` VARCHAR(100) NOT NULL,
  `password` VARCHAR(100) NOT NULL,
  `Email` VARCHAR(50) NOT NULL DEFAULT '0',
  `type` TINYINT(4) NOT NULL DEFAULT '0',
  `money` INT(11) NOT NULL DEFAULT '0',
  `bgood` INT(11) NOT NULL DEFAULT '0',
  `baverage` INT(11) NOT NULL DEFAULT '0',
  `bbad` INT(11) NOT NULL DEFAULT '0',
  `sgood` INT(11) NOT NULL DEFAULT '0',
  `saverage` INT(11) NOT NULL DEFAULT '0',
  `sbad` INT(11) NOT NULL DEFAULT '0',
  `name` VARCHAR(20) NULL DEFAULT NULL,
  `phone` VARCHAR(20) NULL DEFAULT NULL,
  `qq` VARCHAR(15) NULL DEFAULT NULL,
  `order_id` INT(11) NOT NULL,
  `communicate_id` INT(11) NOT NULL,
  PRIMARY KEY (`id`, `communicate_id`),
  UNIQUE INDEX `username` (`username` ASC),
  INDEX `fk_member_order_idx` (`order_id` ASC),
  INDEX `fk_member_communicate1_idx` (`communicate_id` ASC),
  CONSTRAINT `fk_member_communicate1`
    FOREIGN KEY (`communicate_id`)
    REFERENCES `handicrafts`.`communicate` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_member_order`
    FOREIGN KEY (`order_id`)
    REFERENCES `handicrafts`.`order` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `handicrafts`.`order_has_crafts`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `handicrafts`.`order_has_crafts` (
  `order_id` INT(11) NOT NULL,
  `crafts_id` INT(11) NOT NULL,
  PRIMARY KEY (`order_id`, `crafts_id`),
  INDEX `fk_order_has_crafts_crafts1_idx` (`crafts_id` ASC),
  INDEX `fk_order_has_crafts_order1_idx` (`order_id` ASC),
  CONSTRAINT `fk_order_has_crafts_crafts1`
    FOREIGN KEY (`crafts_id`)
    REFERENCES `handicrafts`.`crafts` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_order_has_crafts_order1`
    FOREIGN KEY (`order_id`)
    REFERENCES `handicrafts`.`order` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `handicrafts`.`store`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `handicrafts`.`store` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `itemid` INT(11) NOT NULL,
  `userid` INT(11) NOT NULL,
  `order_id` INT(11) NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_store_order1_idx` (`order_id` ASC),
  CONSTRAINT `fk_store_order1`
    FOREIGN KEY (`order_id`)
    REFERENCES `handicrafts`.`order` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;


-- -----------------------------------------------------
-- Table `handicrafts`.`groupChou`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `handicrafts`.`groupChou` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `title` VARCHAR(45) NULL,
  `num` INT NULL,
  `subtitle` VARCHAR(45) NULL,
  `description` VARCHAR(45) NULL,
  `beginTime` VARCHAR(45) NULL,
  `endTime` VARCHAR(45) NULL,
  `img` VARCHAR(45) NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;

```


## 创新点

+ 项目创新点在于嵌入了Intel RealSense 手势识别技术用以登陆验证，代替繁复的验证码输入，提高用户体验
+ md5加密技术


