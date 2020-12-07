---
description: SqlServerAlias クラス
title: SqlServerAlias クラス
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- SqlServerAlias Class
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServerAlias class
ms.assetid: 475662b9-6985-45bf-b1e9-b0f26ef50443
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 48ecf56931682da1ba0cc7ee1e379ad5146479db
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891632"
---
# <a name="sqlserveralias-class"></a>SqlServerAlias クラス
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [SqlServerAlias class](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)クラスは、サーバー接続の別名を表します。  
  
 サーバー接続別名は、次の両方に該当する場合に必要となります。  
  
-   クライアントが、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 既定のネットワーク転送ではないネットワークトランスポート経由でのインスタンスに接続しています。  
  
-   クライアントが接続されている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスが代替の名前付きパイプをリッスンする場合。  
  
 **注:**[SqlServerAlias クラス](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)は、プロバイダークラスから**Put**メソッドを継承します。 ただし、 **プロバイダー::P ut** メソッドによって示される結果は返されません。 詳細については、WMI のドキュメントを参照してください。  
  
## <a name="see-also"></a>参照  
 [クライアント プロトコルの構成](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
