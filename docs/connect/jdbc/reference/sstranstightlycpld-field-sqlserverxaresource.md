---
description: SSTRANSTIGHTLYCPLD フィールド (SQLServerXAResource)
title: SSTRANSTIGHTLYCPLD フィールド (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apilocation:
- SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apitype: Assembly
ms.assetid: 379857c3-9de1-4964-8782-32df317cbfbb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f3161ceb41586e330bee39206700702cf3d36239
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431554"
---
# <a name="sstranstightlycpld-field-sqlserverxaresource"></a>SSTRANSTIGHTLYCPLD フィールド (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  XA ブランチ トランザクション ID (XID) は異なるが、グローバル トランザクション ID (GTRID) が同じである、密に結合された XA トランザクションを許可するために使用します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public static final int SSTRANSTIGHTLYCPLD  
```  
  
## <a name="field-value"></a>フィールド値  
 **int** 値 32768。  
  
## <a name="remarks"></a>解説  
 各トランザクションは、XA ブランチ トランザクション ID (XID) およびグローバル トランザクション ID (GTRID) によって識別されます。 XID は異なるが GTRID が同じである、密に結合された XA トランザクションをアプリケーションで使用できるようにするには、XAResource.start メソッドの flags パラメーターに [SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) を設定する必要があります。 このフラグの使用方法の詳細については、「[XA トランザクションについて](../../../connect/jdbc/understanding-xa-transactions.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLServerXAResource のフィールド](../../../connect/jdbc/reference/sqlserverxaresource-fields.md)   
 [SQLServerXAResource のメンバー](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource クラス](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
