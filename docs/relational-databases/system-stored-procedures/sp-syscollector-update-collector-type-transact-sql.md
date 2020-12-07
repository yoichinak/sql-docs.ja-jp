---
description: sp_syscollector_update_collector_type (Transact-SQL)
title: sp_syscollector_update_collector_type (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collector_type_TSQL
- sp_syscollector_update_collector_type
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_update_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 3c414dfd-d9ca-4320-81aa-949465b967bf
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 175e3299c37afe307de8b5f809e44646d0a26047
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534850"
---
# <a name="sp_syscollector_update_collector_type-transact-sql"></a>sp_syscollector_update_collector_type (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  コレクション項目のコレクター型を更新します。 コレクター型の名前と GUID を指定すると、によって、コレクションとアップロードパッケージ、パラメータースキーマ、およびパラメーターフォーマッタスキーマを含むコレクター型の構成が更新されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_update_collector_type [ @collector_type_uid = ] 'collector_type_uid' OUTPUT  
          , [ @name = ] 'name'  
          , [ @parameter_schema = ] 'parameter_schema'  
          , [ @collection_package_id = ] collection_package_id  
          , [ @upload_package_id = ] upload_package_id  
```  
  
## <a name="arguments"></a>引数  
`[ @collector_type_uid = ] 'collector_type_uid'` コレクター型の GUID を示します。 *collector_type_uid* は **UNIQUEIDENTIFIER**です。 NULL の場合は、自動的に作成され、出力として返されます。  
  
`[ @name = ] 'name'` コレクター型の名前を指定します。 *名前* は **sysname** ので、指定する必要があります。  
  
`[ @parameter_schema = ] 'parameter_schema'` このコレクター型の XML スキーマです。 *parameter_schema* は **xml** であり、特定のコレクター型で必要になる場合があります。 必須ではない場合、この引数は NULL にすることができます。  
  
`[ @collection_package_id = ] collection_package_id`[!INCLUDE[ssIS](../../includes/ssis-md.md)]コレクションセットによって使用されるコレクションパッケージを指すローカル一意識別子です。 *collection_package_id* は **uniqueidentifer** であり、必須です。 *Collection_package_id*の値を取得するには、msdb データベースの dbo.syscollector_collector_types システムビューに対してクエリを実行します。  
  
`[ @upload_package_id = ] upload_package_id`[!INCLUDE[ssIS](../../includes/ssis-md.md)]コレクションセットによって使用されるアップロードパッケージを指すローカル一意識別子です。 *upload_package_id* は **uniqueidentifier** であり、必須です。 *Upload_package_id*の値を取得するには、msdb データベースの dbo.syscollector_collector_types システムビューに対してクエリを実行します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 **Dc_admin** (EXECUTE 権限を持つ) 固定データベースロールのメンバーシップが必要です。  
  
## <a name="example"></a>例  
 次の例では、ジェネリック T-SQL Query コレクター型を更新します  (この例では、ジェネリック T-SQL Query コレクター型の既定のスキーマを使用しています)。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collector_type  
@collector_type_uid = '302E93D1-3424-4BE7-AA8E-84813ECF2419',  
@name = 'Generic T-SQL Query Collector Type',  
@parameter_schema = '<?xml version="1.0" encoding="utf-8"?>  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" targetNamespace="DataCollectorType">  
  <xs:element name="TSQLQueryCollector">  
<xs:complexType>  
  <xs:sequence>  
<xs:element name="Query" minOccurs="1" maxOccurs="unbounded">  
  <xs:complexType>  
<xs:sequence>  
  <xs:element name="Value" type="xs:string" />  
  <xs:element name="OutputTable" type="xs:string" />  
</xs:sequence>  
  </xs:complexType>  
</xs:element>  
<xs:element name="Databases" minOccurs="0" maxOccurs="1">  
  <xs:complexType>  
<xs:sequence>  
  <xs:element name="Database" minOccurs="0" maxOccurs="unbounded" type="xs:string" />  
</xs:sequence>  
<xs:attribute name="UseSystemDatabases" type="xs:boolean" use="optional" />  
<xs:attribute name="UseUserDatabases" type="xs:boolean" use="optional" />  
  </xs:complexType>  
</xs:element>  
  </xs:sequence>  
</xs:complexType>  
  </xs:element>  
</xs:schema>',  
@collection_package_id = '292B1476-0F46-4490-A9B7-6DB724DE3C0B',  
@upload_package_id = '6EB73801-39CF-489C-B682-497350C939F0';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
