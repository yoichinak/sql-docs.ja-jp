---
description: setResponseBuffering メソッド (SQLServerStatement)
title: setResponseBuffering メソッド (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: 9f489835-6cda-4c8c-b139-079639a169cf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fecbee60be6ffe48ffd72d66bf12e78de40a93c5
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99178663"
---
# <a name="setresponsebuffering-method-sqlserverstatement"></a>setResponseBuffering メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトの応答バッファリング モードを **String full** または **adaptive** に設定します。これらのモードの文字列では、大文字と小文字のどちらも使用できます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *value*  
  
 応答バッファリング モードを含む **String** です。 有効なモードは **full** または **adaptive** のいずれかです。モードを表すこれらの文字列では、大文字と小文字のどちらも使用できます。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 **adaptive** 値は、必要に応じて最小限のデータをバッファリングすることを示します。  
  
 **full** は、実行時にサーバーから結果全体を読み取ることを示します。  
  
 adaptive は、JDBC ドライバー バージョン 2.0 および 3.0 の既定値です。 JDBC ドライバー バージョン 2.0 より前の既定値は full でした。  
  
 [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) メソッドを使用すると、現在の [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトの **responseBuffering** 接続の **String** プロパティをオーバーライドできます。 応答バッファリング モードの使用方法の詳細については、「[アダプティブ バッファリングの使用](../../../connect/jdbc/using-adaptive-buffering.md)」を参照してください。  
  
 アプリケーションで [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) メソッドに無効なパラメーター値が指定された場合は、[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) がスローされます。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)   
 [アダプティブ バッファリングの使用](../../../connect/jdbc/using-adaptive-buffering.md)  
  
  
