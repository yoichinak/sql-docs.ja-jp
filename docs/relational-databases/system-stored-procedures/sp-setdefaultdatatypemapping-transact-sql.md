---
description: sp_setdefaultdatatypemapping (Transact-sql)
title: sp_setdefaultdatatypemapping (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setdefaultdatatypemapping
- sp_setdefaultdatatypemapping_TSQL
helpviewer_keywords:
- sp_setdefaultdatatypemapping
ms.assetid: 7394e8ca-4ce1-4e99-a784-205007c2c248
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6a712ecb629090947b0612844ce6049540b7359a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534955"
---
# <a name="sp_setdefaultdatatypemapping-transact-sql"></a>sp_setdefaultdatatypemapping (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と以外のデータベース管理システム (DBMS) の間の既存のデータ型マッピングを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 既定値としてマークします。 このストアドプロシージャは、ディストリビューター側で任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_setdefaultdatatypemapping [ [ @mapping_id = ] mapping_id ]  
    [ , [ @source_dbms = ] 'source_dbms' ]  
    [ , [ @source_version = ] 'source_version' ]  
    [ , [ @source_type = ] 'source_type' ]   
    [ , [ @source_length_min = ] source_length_min ]  
    [ , [ @source_length_max = ] source_length_max ]  
    [ , [ @source_precision_min = ] source_precision_min ]  
    [ , [ @source_precision_max = ] source_precision_max ]  
    [ , [ @source_scale_min = ] source_scale_min ]  
    [ , [ @source_scale_max = ] source_scale_max ]  
    [ , [ @source_nullable = ] source_nullable ]  
    [ , [ @destination_dbms = ] 'destination_dbms' ]  
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' ]  
    [ , [ @destination_length = ] destination_length ]  
    [ , [ @destination_precision = ] destination_precision ]  
    [ , [ @destination_scale = ] destination_scale ]  
    [ , [ @destination_nullable = ] source_nullable ]  
```  
  
## <a name="arguments"></a>引数  
`[ @mapping_id = ] mapping_id` 既存のデータ型マッピングを識別します。  *mapping_id* は **int**,、既定値は NULL です。 *Mapping_id*を指定した場合、残りのパラメーターは必要ありません。  
  
`[ @source_dbms = ] 'source_dbms'` データ型のマップ元となる DBMS の名前を指定します。 *source_dbms* は **sysname**で、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**MSSQLSERVER**|ソースは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースです。|  
|**ORACLE11I**|マップ元は Oracle データベース。|  
|NULL (既定値)||  
  
 *Mapping_id*が NULL の場合は、このパラメーターを指定する必要があります。  
  
`[ @source_version = ] 'source_version'` ソース DBMS のバージョン番号を指定します。 *source_version* は **varchar (10)**,、既定値は NULL です。  
  
`[ @source_type = ] 'source_type'` は、ソース DBMS のデータ型です。 *source_type* は **sysname**です。 *Mapping_id*が NULL の場合は、このパラメーターを指定する必要があります。  
  
`[ @source_length_min = ] source_length_min` ソース DBMS でのデータ型の最小長を示します。 *source_length_min* は **bigint**,、既定値は NULL です。  
  
`[ @source_length_max = ] source_length_max` ソース DBMS でのデータ型の最大長です。 *source_length_max* は **bigint**,、既定値は NULL です。  
  
`[ @source_precision_min = ] source_precision_min` ソース DBMS でのデータ型の最小有効桁数です。 *source_precision_min* は **bigint**,、既定値は NULL です。  
  
`[ @source_precision_max = ] source_precision_max` ソース DBMS でのデータ型の最大有効桁数です。 *source_precision_max* は **bigint**,、既定値は NULL です。  
  
`[ @source_scale_min = ] source_scale_min` は、ソース DBMS でのデータ型の最小小数点以下桁数です。 *source_scale_min* は **int**,、既定値は NULL です。  
  
`[ @source_scale_max = ] source_scale_max` ソース DBMS でのデータ型の最大小数点以下桁数です。 *source_scale_max* は **int**,、既定値は NULL です。  
  
`[ @source_nullable = ] source_nullable` ソース DBMS のデータ型が NULL 値をサポートするかどうかを指定します。 *source_nullable* は **ビット**,、既定値は NULL です。 **1** は、NULL 値がサポートされていることを示します。  
  
`[ @destination_dbms = ] 'destination_dbms'` マップ先 DBMS の名前を指定します。 *destination_dbms* は **sysname**で、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**MSSQLSERVER**|マップ先は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース。|  
|**ORACLE11I**|変換先は、Oracle データベースです。|  
|**DB2**|マップ先は IBM DB2 データベース。|  
|**SYBASE**|コピー先は Sybase データベースです。|  
|NULL (既定値)||  
  
`[ @destination_version = ] 'destination_version'` マップ先 DBMS の製品バージョンを指定します。 *destination_version* は **varchar (10)**,、既定値は NULL です。  
  
`[ @destination_type = ] 'destination_type'` マップ先 DBMS に表示されるデータ型です。 *destination_type* は **sysname**で、既定値は NULL です。  
  
`[ @destination_length = ] destination_length` マップ先 DBMS でのデータ型の長さを指定します。 *destination_length* は **bigint**,、既定値は NULL です。  
  
`[ @destination_precision = ] destination_precision` マップ先 DBMS でのデータ型の有効桁数です。 *destination_precision* は **bigint**,、既定値は NULL です。  
  
`[ @destination_scale = ] destination_scale` マップ先 DBMS でのデータ型の小数点以下桁数です。 *destination_scale* は **int**,、既定値は NULL です。  
  
`[ @destination_nullable = ] destination_nullable` マップ先 DBMS のデータ型が NULL 値をサポートするかどうかを指定します。 *destination_nullable* は **ビット**,、既定値は NULL です。 **1** は、NULL 値がサポートされていることを示します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_setdefaultdatatypemapping** は、と以外の DBMS の間のすべての種類のレプリケーションで使用され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 既定のデータ型マッピングは、指定した DBMS を含むすべてのレプリケーション トポロジに適用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_setdefaultdatatypemapping**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [Oracle パブリッシャーのデータ型マッピングの指定](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [sp_getdefaultdatatypemapping &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_helpdatatypemap &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
