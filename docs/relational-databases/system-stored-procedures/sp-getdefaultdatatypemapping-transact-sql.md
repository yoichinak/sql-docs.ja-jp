---
description: sp_getdefaultdatatypemapping (Transact-SQL)
title: sp_getdefaultdatatypemapping (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getdefaultdatatypemapping_TSQL
- sp_getdefaultdatatypemapping
helpviewer_keywords:
- sp_getdefaultdatatypemapping
ms.assetid: b8401de1-f135-41d0-ba79-ce8fe1f48c00
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6d7737d0c4d8d44901da52bad6ad6867d7080554
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543342"
---
# <a name="sp_getdefaultdatatypemapping-transact-sql"></a>sp_getdefaultdatatypemapping (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と以外の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース管理システム (DBMS) 間の、指定されたデータ型の既定のマッピングに関する情報を返します。 このストアドプロシージャは、ディストリビューター側で任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_getdefaultdatatypemapping [ @source_dbms = ] 'source_dbms'   
    [ , [ @source_version = ] 'source_version' ]  
        , [ @source_type = ] 'source_type'    
    [ , [ @source_length = ] source_length ]  
    [ , [ @source_precision = ] source_precision ]  
    [ , [ @source_scale = ] source_scale ]  
    [ , [ @source_nullable = ] source_nullable ]  
        , [ @destination_dbms = ] 'destination_dbms'   
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' OUTPUT ]  
    [ , [ @destination_length = ] destination_length OUTPUT ]  
    [ , [ @destination_precision = ] destination_precision OUTPUT ]  
    [ , [ @destination_scale = ] destination_scale OUTPUT ]  
    [ , [ @destination_nullable = ] source_nullable OUTPUT ]  
    [ , [ @dataloss = ] dataloss OUTPUT ]  
```  
  
## <a name="arguments"></a>引数  
`[ @source_dbms = ] 'source_dbms'` データ型のマップ元となる DBMS の名前を指定します。 *source_dbms* は **sysname**で、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**MSSQLSERVER**|ソースは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースです。|  
|**ORACLE11I**|マップ元は Oracle データベース。|  
  
 このパラメーターを指定する必要があります。  
  
`[ @source_version = ] 'source_version'` ソース DBMS のバージョン番号を指定します。 *source_version* は **varchar (10)**,、既定値は NULL です。  
  
`[ @source_type = ] 'source_type'` は、ソース DBMS のデータ型です。 *source_type* は **sysname**であり、既定値はありません。  
  
`[ @source_length = ] source_length` ソース DBMS のデータ型の長さを示します。 *source_length* は **bigint**,、既定値は NULL です。  
  
`[ @source_precision = ] source_precision` ソース DBMS のデータ型の有効桁数です。 *source_precision* は **bigint**,、既定値は NULL です。  
  
`[ @source_scale = ] source_scale` ソース DBMS でのデータ型の小数点以下桁数です。 *source_scale* は **int**,、既定値は NULL です。  
  
`[ @source_nullable = ] source_nullable` ソース DBMS のデータ型が NULL 値をサポートするかどうかを指定します。 *source_nullable* の部分は **ビット**で、既定値は **1**です。これは、NULL 値がサポートされることを意味します。  
  
`[ @destination_dbms = ] 'destination_dbms'` マップ先 DBMS の名前を指定します。 *destination_dbms* は **sysname**で、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**MSSQLSERVER**|マップ先は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース。|  
|**ORACLE11I**|変換先は、Oracle データベースです。|  
|**DB2**|マップ先は IBM DB2 データベース。|  
|**SYBASE**|コピー先は Sybase データベースです。|  
  
 このパラメーターを指定する必要があります。  
  
`[ @destination_version = ] 'destination_version'` マップ先 DBMS の製品バージョンを指定します。 *destination_version* は **varchar (10)**,、既定値は NULL です。  
  
`[ @destination_type = ] 'destination_type' OUTPUT` マップ先 DBMS に表示されるデータ型です。 *destination_type* は **sysname**で、既定値は NULL です。  
  
`[ @destination_length = ] destination_length OUTPUT` マップ先 DBMS でのデータ型の長さを指定します。 *destination_length* は **bigint**,、既定値は NULL です。  
  
`[ @destination_precision = ] destination_precision OUTPUT` マップ先 DBMS でのデータ型の有効桁数です。 *destination_precision* は **bigint**,、既定値は NULL です。  
  
`[ @destination_scale = ] _destination_scaleOUTPUT` マップ先 DBMS でのデータ型の小数点以下桁数です。 *destination_scale* は **int**,、既定値は NULL です。  
  
`[ @destination_nullable = ] _destination_nullableOUTPUT` マップ先 DBMS のデータ型が NULL 値をサポートするかどうかを指定します。 *destination_nullable* は **ビット**,、既定値は NULL です。 **1** は、NULL 値がサポートされていることを示します。  
  
`[ @dataloss = ] _datalossOUTPUT` マッピングがデータ損失の可能性があるかどうかを示します。 *データ損失* は **ビット**,、既定値は NULL です。 **1** は、データ損失の可能性があることを意味します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_getdefaultdatatypemapping** は、と以外の DBMS の間のすべての種類のレプリケーションで使用され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 **sp_getdefaultdatatypemapping** は、指定された変換元データ型に最も一致する、既定の変換先データ型を返します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_getdefaultdatatypemapping**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_helpdatatypemap &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)   
 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md)  
  
  
