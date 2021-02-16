---
title: " ADR クリーナー再試行タイムアウト (分) 構成オプション | Microsoft Docs"
description: ADR クリーナーの再試行タイムアウトの SQL Server インスタンス構成設定について説明します。
ms.custom: ''
ms.date: 06/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ADR cleaner retry timeout (min)
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 05502bbf760b0f8aa18d81739ce89e19e92397cb
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100347473"
---
# <a name="adr-cleaner-retry-timeout-min-configuration-option"></a>ADR クリーナー再試行タイムアウト (分) 構成オプション

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

SQL Server 2019 で導入されました。

この構成設定は、[高速データベース回復](../../relational-databases/accelerated-database-recovery-concepts.md)に必要です。 クリーナーは、定期的に起動し、不要なページ バージョンを消去する非同期プロセスです。

場合によっては、オブジェクト レベルのロックを取得するときに、スイープ中のユーザー ワークロードとの競合が原因でクリーナーの問題が発生することがあります。 クリーナーは、このようなページを個別のリストで追跡します。 ADR クリーナーの再試行タイムアウト (既定値は 15) は、スイープを破棄する前に、クリーナーがオブジェクト ロックの取得とページのクリーンアップを排他的に再試行する時間を制御します。 中止されたトランザクションのマップで中止されたトランザクションの増加を維持するには、100% 成功したスイープの完了が不可欠です。 指定されたタイムアウトで個別のリストをクリーンアップできない場合、現在のスイープは破棄され、次のスイープが開始されます。

## <a name="remarks"></a>解説  

クリーナーは SQL Server 2019 のシングル スレッドであるため、1 つの SQL Server インスタンスは一度に 1 つのデータベースで作業できます。 インスタンスに ADR が有効になっているユーザー データベースが複数存在する場合は、別のデータベースで再試行が行われている間に、1 つのデータベースでのクリーンアップが遅延する可能性があるため、タイムアウトを大きな値に増やすことはできません。

## <a name="examples"></a>例

次の例は、クリーナーの再試行タイムアウトを設定します。

```tsql
sp_configure 'show advanced options', 1;  
RECONFIGURE;
GO 
sp_configure 'ADR cleaner retry timeout', 15;  
RECONFIGURE;  
GO  
```  

## <a name="see-also"></a>参照  

- [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [データベース復旧の高速化](../../relational-databases/accelerated-database-recovery-concepts.md)
- [高速データベース復旧の管理](../../relational-databases/accelerated-database-recovery-management.md)