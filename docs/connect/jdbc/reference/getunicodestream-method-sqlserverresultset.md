---
description: getUnicodeStream メソッド (SQLServerResultSet)
title: getUnicodeStream メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerResultSet.getUnicodeStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0dd61865-663b-47e2-b417-e9df418894cc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b41d27ecf9c4d67d2eb80469948b1f4376863881
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99155038"
---
# <a name="getunicodestream-method-sqlserverresultset"></a>getUnicodeStream メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、Unicode 文字のストリームとして取得されます。  
  
> [!NOTE]  
>  このメソッドは、JDBC 仕様で非推奨とされます。このメソッドを呼び出すと、"未実装" 例外がスローされます。 代わりに、[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) メソッドを使用する必要があります。  
  
## <a name="overload-list"></a>オーバーロードの一覧  
  
|名前|説明|  
|----------|-----------------|  
|[getUnicodeStream メソッド &#40;int&#41;](../../../connect/jdbc/reference/getunicodestream-method-int.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列インデックスの値を、Unicode 文字のストリームとして取得します。|  
|[getUnicodeStream メソッド &#40;java.lang.String&#41;](../../../connect/jdbc/reference/getunicodestream-method-java-lang-string.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列名の値を、Unicode 文字のストリームとして取得します。|  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
