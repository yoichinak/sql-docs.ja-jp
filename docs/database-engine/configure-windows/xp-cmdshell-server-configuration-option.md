---
title: xp_cmdshell サーバー構成オプション
description: "\"xp_cmdshell\" オプションについて説明します。 SQL Server で \"xp_cmdshell\" 拡張ストアド プロシージャを実行できるかどうかが、これによってどのように制御されるかを確認します。 これを有効にする方法について説明します。"
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- xp_cmdshell
ms.assetid: c147c9e1-b81d-49c8-b800-3019f4d86a13
author: markingmyname
ms.author: maghan
ms.custom: contperfq4
ms.date: 06/12/2020
ms.openlocfilehash: 004a7b0a50a657632bb2b9970f0558857d416494
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257977"
---
# <a name="xp_cmdshell-server-configuration-option"></a>xp_cmdshell サーバー構成オプション

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

この記事では、 **xp_cmdshell** SQL Server 構成オプションを有効にする方法について説明します。 システム管理者はこのオプションを使用して、[xp_cmdshell 拡張ストアド プロシージャ](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md)をシステムで実行できるかどうかを制御できます。 新規インストールの場合、 **xp_cmdshell** オプションは既定で無効になっています。

このオプションを有効にする前に、潜在的なセキュリティの影響を考慮することが重要です。

- 新しく開発されたコードでは、 **xp_cmdshell** ストアド プロシージャを使用しないでください。通常は、無効のままにしておく必要があります。
- 一部のレガシ アプリケーションでは、 **xp_cmdshell** を有効にする必要があります。 このストアド プロシージャを使用しないようにアプリケーションを変更できない場合は、以下の説明に従って有効にすることができます。

> [!NOTE]  
> **xp_cmdshell** を使用する必要がある場合、セキュリティのベスト プラクティスとして、それを必要とする実際のタスクの期間だけそれを有効にすることをお勧めします。

**xp_cmdshell** を有効にする必要がある場合は、 [ポリシーベースの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)を使用するか、次のコード例に示すように **sp_configure** システム ストアド プロシージャを実行します。  
  
``` sql
-- To allow advanced options to be changed.  
EXECUTE sp_configure 'show advanced options', 1;  
GO  
-- To update the currently configured value for advanced options.  
RECONFIGURE;  
GO  
-- To enable the feature.  
EXECUTE sp_configure 'xp_cmdshell', 1;  
GO  
-- To update the currently configured value for this feature.  
RECONFIGURE;  
GO  
```  
  
## <a name="next-steps"></a>次のステップ

- [xp_cmdshell 拡張ストアド プロシージャ](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md)
- [サーバー構成オプション (SQL Server)](server-configuration-options-sql-server.md)
- [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
