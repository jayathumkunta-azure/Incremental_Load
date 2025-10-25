# Incremental_Load
# pipeline level
select  watermarkvalue from watermarktable where tablename='StateProvince_source'


# Database
CREATE TABLE StateProvince_Source(
    [StateProvinceID] [int] NOT NULL,
    [StateProvinceCode] [nchar](3) NOT NULL,
    [CountryRegionCode] [nvarchar](3) NOT NULL,
    [IsOnlyStateProvinceFlag] int NOT NULL,
    [Name] [nchar](100) NOT NULL,
    [TerritoryID] [int] NOT NULL,
    [rowguid] [nvarchar](100)  NOT NULL,
    [ModifiedDate] [datetime] NOT NULL)

CREATE TABLE StateProvince_Target(
    [StateProvinceID] [int] NOT NULL,
    [StateProvinceCode] [nchar](3) NOT NULL,
    [CountryRegionCode] [nvarchar](3) NOT NULL,
    [IsOnlyStateProvinceFlag] int NOT NULL,
    [Name] [nchar](100) NOT NULL,
    [TerritoryID] [int] NOT NULL,
    [rowguid] [nvarchar](100)  NOT NULL,
    [ModifiedDate] [datetime] NOT NULL)




INSERT INTO [dbo].[StateProvince] ([StateProvinceID],[StateProvinceCode] ,[CountryRegionCode]    ,[IsOnlyStateProvinceFlag],[Name]  ,[TerritoryID],[rowguid] ,[ModifiedDate])
values ('10','CO',  'US',     '0', 'Colorado'                 ,'3',   '292DF595-7D3C-41FB-A040-7C184D379FCE', '2015-02-08 10:17:21.587')

INSERT INTO [dbo].[StateProvince] ([StateProvinceID],[StateProvinceCode] ,[CountryRegionCode]    ,[IsOnlyStateProvinceFlag],[Name]  ,[TerritoryID],[rowguid] ,[ModifiedDate])
values(11 ,'CT',    'US',     '0', 'Connecticut'          ,'2',  '1E7BB47A-E16B-4968-86FA-45AF0211FA84', '2025-02-08 10:17:21.587')

----------------------------  
INSERT INTO [dbo].[StateProvince] ([StateProvinceID],[StateProvinceCode] ,[CountryRegionCode]    ,[IsOnlyStateProvinceFlag],[Name]  ,[TerritoryID],[rowguid] ,[ModifiedDate])
values(12 ,'DC',    'US',     '0', 'District of Columbia'   ,'2',     'A1F3C57E-85B3-41E3-88E8-07244CF087DD', '2025-7-08 10:17:21.587')

INSERT INTO [dbo].[StateProvince] ([StateProvinceID],[StateProvinceCode] ,[CountryRegionCode]    ,[IsOnlyStateProvinceFlag],[Name]  ,[TerritoryID],[rowguid] ,[ModifiedDate])
     VALUES (3,     'AL'      ,'US'     ,'0',     'Alabama',               5    ,'41B328BE-21AE-45D0-841D-6F8DD71CE626',     '2026-09-08 10:17:21.587')
INSERT INTO [dbo].[StateProvince] ([StateProvinceID],[StateProvinceCode] ,[CountryRegionCode]    ,[IsOnlyStateProvinceFlag],[Name]  ,[TerritoryID],[rowguid] ,[ModifiedDate])
     VALUES(4, 'AR'      ,'US'     ,'0',     'Arkansas',              3    ,'54656A80-06F2-4C70-BA10-247179FC246E',     '2014-02-08 10:17:21.587')


-----------------------------
create table watermarktable
(
tablename varchar(255),
watermarkvalue datetime

)
insert into watermarktable(tablename,watermarkvalue)
values('StateProvince_Source','1990-02-08 10:17:21.587')

create procedure updateinfo
as
begin
update  watermarktable 
set watermarkvalue=(select  max(ModifiedDate) from StateProvince_Source)
where tablename='StateProvince_Source'
end
