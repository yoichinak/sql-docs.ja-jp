---
description: sp_cdc_disable_table (Transact-sql)
title: sp_cdc_disable_table (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_disable_table
- sp_cdc_disable_table
- sys.sp_cdc_disable_table_TSQL
- sp_cdc_disable_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_disable_table
- sys.sp_cdc_disable_table
- change data capture [SQL Server], disabling tables
ms.assetid: da2156c0-504e-4d76-b9a0-4448becf9bda
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f0819c156cdc3e836028915d89a8d9100eef17c6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541161"
---
# <a name="syssp_cdc_disable_table-transact-sql"></a>sp_cdc_disable_table (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベース内の指定したソーステーブルおよびキャプチャインスタンスの変更データキャプチャを無効にします。 変更データ キャプチャは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディッションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_disable_table   
  [ @source_schema = ] 'source_schema' ,   
  [ @source_name = ] 'source_name'  
  [ , [ @capture_instance = ] 'capture_instance' | 'all' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @source_schema = ] 'source\_schema'` ソーステーブルが含まれているスキーマの名前を指定します。 *source_schema* は **sysname**であり、既定値はありません。 NULL にすることはできません。  
  
 *source_schema* は、現在のデータベースに存在している必要があります。  
  
`[ @source_name = ] 'source\_name'` 変更データキャプチャを無効にするソーステーブルの名前を指定します。 *source_name* は **sysname**であり、既定値はありません。 NULL にすることはできません。  
  
 *source_name* は、現在のデータベースに存在している必要があります。  
  
`[ @capture_instance = ] 'capture\_instance' | 'all'` 指定したソーステーブルに対して無効にするキャプチャインスタンスの名前を指定します。 *capture_instance* は **sysname** であり、NULL にすることはできません。  
  
 ' All ' を指定した場合、 *source_name* に対して定義されているすべてのキャプチャインスタンスは無効になります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 指定したソーステーブルおよびキャプチャインスタンスに関連付けられている変更データキャプチャの変更テーブルとシステム関数を削除するには、sp_cdc_disable_table によって削除され**ます。** このメソッドは、指定されたキャプチャインスタンスに関連付けられているすべての行を変更データキャプチャのシステムテーブルから削除し、テーブルのエントリの **is_tracked_by_cdc** 列を、 [テーブルカタログビュー](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) を0に設定します。  
  
## <a name="permissions"></a>アクセス許可  
 **Db_owner**固定データベースロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、テーブルの変更データキャプチャを無効にし `HumanResources.Employee` ます。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_disable_table   
    @source_schema = N'HumanResources',   
    @source_name = N'Employee',  
    @capture_instance = N'HumanResources_Employee';  
```  
  
## <a name="see-also"></a>参照  
 [sp_cdc_enable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)  
  
  
