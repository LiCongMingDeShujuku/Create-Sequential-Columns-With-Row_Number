![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 使用Row_Number创建顺序列
#### Create Sequential Columns With Row_Number
**发布-日期: 2018年02月01日 (评论)**

![#](images/create-sequential-columns-with-row-number.png?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
有时你会发现自己需要创建大量列来导入表，下面我用row_number（）函数在表中创建各种顺序行（row）的快速技巧。

## English
Sometimes you find yourself needing to create massive columns for import tables, and here’s a quick trick I use to create a variety of sequential rows in tables using the row_number() function. 

---
## Logic
```SQL
use master;
set nocount on
 
declare @make_many_columns  table ([column_name] varchar(255))
insert into @make_many_columns
select
    case
        when row_number() over(order by [id] asc) < 100 then ',  [Column_00' + cast(row_number() over(order by [id] asc) as varchar(10)) + '] varchar(max)'
        else ', [Column_' + cast(row_number() over(order by [id] asc) as varchar(10)) + '] varchar(max)'
    end as 'Row'
from
    sysobjects
 
select top 200 * from @make_many_columns
 
create table [MyImport_01]
(
-- insert column names here
--在此插入列的名称


```

希望对你有用。 (Hope you find it useful.)

[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

