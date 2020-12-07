---
description: sp_helpdatatypemap (Transact-sql)
title: sp_helpdatatypemap (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdatatypemap
- sp_helpdatatypemap_TSQL
helpviewer_keywords:
- sp_helpdatatypemap
ms.assetid: 800c9c65-723e-4961-a63d-327987f129f0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7fb7ee524e2b9849c9c8a348cd6c8a9de7fb74e2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538779"
---
# <a name="sp_helpdatatypemap-transact-sql"></a>sp_helpdatatypemap (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース管理システム (DBMS) の間の定義済みデータ型マッピングに関する情報を返します。 このストアドプロシージャは、ディストリビューター側で任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpdatatypemap [ @source_dbms = ] 'source_dbms'   
    [ , [ @source_version = ] 'source_version' ]  
    [ , [ @source_type = ] 'source_type' ]   
    [ , [ @destination_dbms = ] 'destination_dbms' ]  
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' ]  
    [ , [ @defaults_only = ] defaults_only ]  
```  
  
## <a name="arguments"></a>引数  
`[ @source_dbms = ] 'source_dbms'` データ型のマップ元となる DBMS の名前を指定します。 *source_dbms* は **sysname**で、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**MSSQLSERVER**|ソースは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースです。|  
|**ORACLE11I**|マップ元は Oracle データベース。|  
  
`[ @source_version = ] 'source_version'` は、ソース DBMS の製品バージョンです。 *source_version*は **varchar (10)** です。指定されていない場合は、すべてのバージョンのソース DBMS のデータ型マッピングが返されます。 値を指定した場合は、マップ元 DBMS のバージョンによって結果セットがフィルター選択されます。  
  
`[ @source_type = ] 'source_type'` は、ソース DBMS に表示されるデータ型です。 *source_type* は **sysname**であり、指定されていない場合は、マップ元 DBMS のすべてのデータ型のマッピングが返されます。 結果セットをソース DBMS のデータ型でフィルター処理できるようにします。  
  
`[ @destination_dbms = ] 'destination_dbms'` マップ先 DBMS の名前を指定します。 *destination_dbms* は **sysname**で、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**MSSQLSERVER**|マップ先は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース。|  
|**ORACLE11I**|変換先は、Oracle データベースです。|  
|**DB2**|マップ先は IBM DB2 データベース。|  
|**SYBASE**|コピー先は Sybase データベースです。|  
  
`[ @destination_version = ] 'destination_version'` マップ先 DBMS の製品バージョンを指定します。 *destination_version*は **varchar (10)** です。指定されていない場合、マップ先 DBMS のすべてのバージョンのマッピングが返されます。 結果セットを DBMS の対象バージョンでフィルター処理できるようにします。  
  
`[ @destination_type = ] 'destination_type'` マップ先 DBMS に表示されるデータ型です。 *destination_type*は **sysname**であり、指定されていない場合は、マップ先 DBMS のすべてのデータ型のマッピングが返されます。 結果セットをマップ先 DBMS のデータ型でフィルター処理できるようにします。  
  
`[ @defaults_only = ] defaults_only` 既定のデータ型マッピングのみが返される場合はです。 *defaults_only* は **ビット**,、既定値は **0**です。 **1** は、既定のデータ型マッピングのみが返されることを意味します。 **0** は、既定のデータ型とユーザー定義データ型のマッピングが返されることを意味します。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|説明|  
|-----------------|-----------------|  
|**mapping_id**|データ型マッピングを識別します。|  
|**source_dbms**|ソース DBMS の名前とバージョン番号を指定します。|  
|**source_type**|は、ソース DBMS のデータ型です。|  
|**destination_dbms**|マップ先 DBMS の名前です。|  
|**destination_type**|マップ先 DBMS のデータ型です。|  
|**is_default**|マッピングが既定または代替マッピングであるかどうかを示します。 値 **0** は、このマッピングがユーザー定義であることを示します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_helpdatatypemap** は、SQL Server 以外のパブリッシャーおよびパブリッシャーから以外のサブスクライバーへのデータ型マッピングを定義し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 指定した変換元と変換先の DBMS の組み合わせがサポートされていない場合、 **sp_helpdatatypemap** は空の結果セットを返します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helpdatatypemap**を実行できるのは、ディストリビューター側の固定サーバーロール**sysadmin**のメンバー、またはディストリビューションデータベースの**db_owner**固定データベースロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_getdefaultdatatypemapping &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)  
  
  
