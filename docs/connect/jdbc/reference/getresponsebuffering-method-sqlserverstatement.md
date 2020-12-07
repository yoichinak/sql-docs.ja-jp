---
description: getResponseBuffering メソッド (SQLServerStatement)
title: getResponseBuffering メソッド (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getResponseBuffering()
apilocation:
- SQLServerStatement.getResponseBuffering()
apitype: Assembly
ms.assetid: a9a9ffdd-7ce3-4e0a-907c-34d6a54e6865
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 08411235fe8e571e9f3bdaf7220f2387d3a0b5c0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434794"
---
# <a name="getresponsebuffering-method-sqlserverstatement"></a>getResponseBuffering メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトの応答バッファリング モードを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>戻り値  
 小文字の **full** または **adaptive** を含む**文字列**です。  
  
## <a name="remarks"></a>解説  
 **adaptive** 値は、必要に応じて最小限のデータをバッファリングすることを示します。  
  
 **full** は、実行時にサーバーから結果全体を読み取ることを示します。  
  
 **adaptive** は、JDBC ドライバー バージョン 2.0 および 3.0 の既定値です。 JDBC ドライバー バージョン 2.0 より前の既定値は **full** でした。  
  
 応答バッファリング モードの使用方法の詳細については、「[アダプティブ バッファリングの使用](../../../connect/jdbc/using-adaptive-buffering.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [setResponseBuffering メソッド &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)   
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
