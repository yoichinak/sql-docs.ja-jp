---
description: setResponseBuffering メソッド (SQLServerDataSource)
title: setResponseBuffering メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: c9e43ff2-8117-4dca-982d-83c863d0c8e1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a62919c7efbefd41505f0ac3e6c021229f3a74d2
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99173172"
---
# <a name="setresponsebuffering-method-sqlserverdatasource"></a>setResponseBuffering メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトを使用して作成された接続の応答バッファリング モードを設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *value*  
  
 バッファリングとストリーミングのモードを含む **文字列** です。 有効なモードは **full** または **adaptive** のいずれかです。モードを表すこれらの文字列では、大文字と小文字のどちらも使用できます。  
  
## <a name="remarks"></a>解説  
 **full** 値は、実行時にサーバーから結果全体を読み取ることを示します。  
  
 **adaptive** 値は、必要に応じて最小限のデータをバッファリングすることを示します。 既定のバッファリング モードは **adaptive** 値です。  
  
 応答バッファリング モードの使用方法の詳細については、「[アダプティブ バッファリングの使用](../../../connect/jdbc/using-adaptive-buffering.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
