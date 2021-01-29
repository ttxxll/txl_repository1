
	2.相关表：net_info，net_info_his新增和编辑时要同时为这两个表进行操作
		ALTER TABLE net_info ADD COLUMN business_region VARCHAR(50) DEFAULT NULL;
		ALTER TABLE net_info_his ADD COLUMN business_region VARCHAR(50) DEFAULT NULL;
    
    网络区域network_region表新增一个字段：environment
		ALTER TABLE network_region ADD COLUMN environment VARCHAR(50) DEFAULT '生产';
    
    net_business_region表删掉regionid字段：
		alter table net_business_region drop column regionid
    
    删除业务区域的机房相关字段：
			ALTER TABLE net_business_region DROP COLUMN address_id;    
			ALTER TABLE net_business_region DROP COLUMN address_name;
      
    1.添加一个中间表来关联网络区域和业务区域：relation
    CREATE TABLE `network_business_relation` (
      `ID` INT(10) NOT NULL AUTO_INCREMENT COMMENT 'id' PRIMARY KEY ,
      `network_id` INT(10) DEFAULT NULL COMMENT '网络区域id',
      `business_id` INT(10) DEFAULT NULL COMMENT '业务区域id'
    )ENGINE=INNODB DEFAULT CHARSET=utf8mb4;
    ALTER TABLE `network_business_relation` ADD COLUMN in_use TINYINT(1) UNSIGNED DEFAULT '0';   
    
    
