---
description: sp_cdc_enable_db (Transact-sql)
title: sp_cdc_enable_db (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_enable_db_TSQL
- sp_cdc_enable_db
- sys.sp_cdc_enable_db
- sys.sp_cdc_enable_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_enable_db
- change data capture [SQL Server], enabling databases
- sp_cdc_enable_db
ms.assetid: 176d83b3-493d-43cd-800e-aa123c3bdf17
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c40d3904737c7740c3658eda12e2f9c9df340b0a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534751"
---
# <a name="syssp_cdc_enable_db-transact-sql"></a>sp_cdc_enable_db (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースの変更データキャプチャを有効にします。 データベース内のテーブルの変更データ キャプチャを有効にするには、まずそのデータベースに対してこの手順を実行する必要があります。 変更データキャプチャは、有効になっているテーブルに適用された挿入、更新、削除の各アクティビティを記録し、変更の詳細を使用しやすいリレーショナル形式で表示します。 追跡対象のソーステーブルの列構造を反映する列情報は、変更された行に対してキャプチャされ、その変更をターゲット環境に適用するために必要なメタデータと共にキャプチャされます。  
  
> [!IMPORTANT]
>  変更データ キャプチャは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディッションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_enable_db  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 [システムデータベース](../../relational-databases/databases/system-databases.md)またはディストリビューションデータベースでは、変更データキャプチャを有効にできません。  
  
 sys.sp_cdc_enable_db を実行すると、メタデータ テーブルや DDL トリガーなど、データベース全体のスコープを持つ変更データ キャプチャ オブジェクトが作成されます。 また、cdc スキーマと cdc データベースユーザーを作成し、データベースエントリの [is_cdc_enabled] 列を [ [sys. データベース](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) ] カタログビューに1に設定します。  
  
## <a name="permissions"></a>アクセス許可  
 sysadmin 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、変更データキャプチャを有効にします。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_enable_db;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_cdc_disable_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md)  
  
  
