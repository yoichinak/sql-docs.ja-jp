---
description: 復旧モデルのエラーを抑制する - サーバー構成オプション
title: 復旧モデルのエラーを抑制する - サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 07/20/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 942dfc62bd55d1843babb78d89b95ad602f3d938
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670745"
---
# <a name="suppress-recovery-model-errors-server-configuration-option"></a>復旧モデルのエラーを抑制する - サーバー構成オプション

[!INCLUDE[tsql-appliesto-xxxxxx-asdbmi-xxxx-xxx-md.md](../../includes/tsql-appliesto-xxxxxx-asdbmi-xxxx-xxx-md.md)]

SQL Server の[復旧モデル](../../relational-databases/backup-restore/recovery-models-sql-server.md)では、トランザクション ログのメンテナンスが制御されます。 完全復旧モデルでは、データ ファイルが失われたり破損したりしたために失われる作業はなく、バックアップ保持ポリシー内の任意の特定の時点への回復がサポートされます。 完全復旧モデルは、SQL Managed Instance でサポートされている既定かつ唯一の復旧モデルです。 SQL Managed Instance で復旧モデルの変更を試みると、エラーメッセージが返されます。

SQL Managed Instance で実行されるデータベース復旧モデルを変更するコマンドがエラーまたは警告のみを返すかどうかを指定するには、 **[Suppress Recovery Model Errors]\(復旧モデルのエラーを抑制する\)** 詳細構成オプションを使用します。 このオプションが SQL Managed Instance で 1 (ON) に設定されている場合は、コマンド ALTER DATABASE SET RECOVERY を実行しても、データベースの復旧モデルは変更されず、エラーは返されませんが、警告メッセージが返されます。 このオプションが SQL Managed Instance で 0 (OFF) に設定されている場合は、コマンド ALTER DATABASE SET RECOVERY を実行するとエラー メッセージが返されます。

**[Suppress Recovery Model Errors]\(復旧モデルのエラーを抑制する\)** オプションは、レガシまたはサードパーティのアプリケーションで、復旧モデルを単純復旧モデルまたは一括ログ復旧モデルに変更しようと試みる場合に役立ちます。ただし、これは重要または必須の要件ではありません。 復旧モデルの変更が SQL Managed Instance の使用に対する唯一の阻害要因である場合は、[Suppress Recovery Model Errors]\(復旧モデルのエラーを抑制する\) 構成オプションをオンにすると、その阻害要因が取り除かれます。 このオプションは、アプリケーション コード変更の別のソリューションが実現できない場合、またはコストが高い場合に特に役立ちます。

## <a name="examples"></a>例

次の例では、データベース復旧モデルの変更に関連するエラー メッセージの抑制を有効にし、データベース復旧モデルを変更するためのコマンドを実行して、警告のみを返します。 復旧モデルは、実際には変更されません。 *my_database* は、実際のデータベース名に置き換えてください。

```sql
-- Turn advanced configuration options on:
sp_configure 'show advanced options', 1 ;  
GO
RECONFIGURE ;  
GO

-- Enable suppression of error messages for recovery model change:
sp_configure 'suppress recovery model errors', 1 ;  
GO
RECONFIGURE ;  
GO

-- Execute command for changing recovery model to Simple:
ALTER DATABASE my_database SET RECOVERY SIMPLE;
GO
```

## <a name="see-also"></a>関連項目

[サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)

[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)

[RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)