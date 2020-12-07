---
description: sp_dsninfo (Transact-SQL)
title: sp_dsninfo (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dsninfo
- sp_dsninfo_TSQL
helpviewer_keywords:
- sp_dsninfo
ms.assetid: 34648615-814b-42bc-95a3-50e86b42ec4d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 451d19531bbee4814fe9335bc4aaba7707263a10
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536102"
---
# <a name="sp_dsninfo-transact-sql"></a>sp_dsninfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のサーバーと関連するディストリビューターから ODBC または OLE DB のデータ ソース情報を返します。 このストアドプロシージャは、ディストリビューター側で任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dsninfo [ @dsn =] 'dsn'   
    [ , [ @infotype =] 'info_type']   
    [ , [ @login =] 'login']   
    [ , [ @password =] 'password']  
    [ , [ @dso_type=] dso_type]  
```  
  
## <a name="arguments"></a>引数  
`[ @dsn = ] 'dsn'` ODBC DSN または OLE DB リンクサーバーの名前を指定します。 *dsn* は **varchar (128)**,、既定値はありません。  
  
`[ @infotype = ] 'info_type'` 返される情報の種類を示します。 *Info_type*が指定されていない場合、または NULL が指定されている場合は、すべての情報の種類が返されます。 *info_type* は **varchar (128)**,、既定値は NULL の場合、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**DBMS_NAME**|データソースのベンダ名を指定します。|  
|**DBMS_VERSION**|データソースのバージョンを指定します。|  
|**DATABASE_NAME**|データベース名を指定します。|  
|**SQL_SUBSCRIBER**|データソースがサブスクライバーであることを指定します。|  
  
`[ @login = ] 'login'` データソースのログインを示します。 データソースにログインが含まれている場合は、NULL を指定するか、パラメーターを省略します。 *ログイン*は **varchar (128)**,、既定値は NULL です。  
  
`[ @password = ] 'password'` ログインのパスワードを入力します。 データソースにログインが含まれている場合は、NULL を指定するか、パラメーターを省略します。 *パスワード*は **varchar (128)**,、既定値は NULL です。  
  
`[ @dso_type = ] dso_type` データソースの種類を入力します。 *dso_type* は **int**,、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1** (既定値)|ODBC データ ソース (ODBC data source)|  
|**3**|OLE DB データ ソース|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**情報の種類**|**nvarchar (64)**|DBMS_NAME、DBMS_VERSION、DATABASE_NAME、SQL_SUBSCRIBER などの情報の種類です。|  
|**Value**|**nvarchar(512)**|関連付けられている情報の種類の値。|  
  
## <a name="remarks"></a>解説  
 **sp_dsninfo** は、すべての種類のレプリケーションで使用されます。  
  
 **sp_dsninfo** は、データベースをレプリケーションまたはクエリに使用できるかどうかを示す ODBC または OLE DB データソース情報を取得します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_dsninfo**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_enumdsn &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-enumdsn-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
