---
description: SQLServerNClob のメンバー
title: SQLServerNClob のメンバー | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: b063f191-175e-4430-aab7-d88907f4ebec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ff734dfb249d7375dc1f92ef03dc53b4679fbf37
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99178146"
---
# <a name="sqlservernclob-members"></a>SQLServerNClob のメンバー
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  次の表は、[SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md) クラスによって公開されるメンバーを示しています。  
  
## <a name="constructors"></a>コンストラクター  
 [なし] :  
  
## <a name="fields"></a>フィールド  
 [なし] :  
  
## <a name="inherited-fields"></a>継承されたフィールド  
 [なし] :  
  
## <a name="methods"></a>メソッド  
  
|名前|説明|  
|----------|-----------------|  
|[free](../../../connect/jdbc/reference/free-method-sqlservernclob.md)|このメソッドは、**NCLOB** オブジェクトと、それが占有していたリソースを解放します。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservernclob.md)|**java.sql.NClob** オブジェクトによって指定された **NCLOB** 値が ASCII ストリームとして取得されます。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)|**java.sql.NClob** オブジェクトによって指定された **NCLOB** 値が取得されます。|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlservernclob.md)|**java.sql.NClob** オブジェクトによって指定された **NCLOB** 値内の指定された部分文字列のコピーが取得されます。|  
|[length](../../../connect/jdbc/reference/length-method-sqlservernclob.md)|**java.sql.NClob** オブジェクトによって指定された **NCLOB** 値の文字数が取得されます。|  
|[position](../../../connect/jdbc/reference/position-method-sqlservernclob.md)|指定された開始位置に基づいて、指定された **java.sql.NClob** オブジェクトまたは **java.sql.NClob** の substring の文字位置を取得します。|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlservernclob.md)|この **java.sql.NClob** オブジェクトが表す **NCLOB** 値の指定された位置から ASCII 文字を書き込むために使用するストリームを取得します。|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservernclob.md)|この **java.sql.NClob** オブジェクトが表す **NCLOB** 値の指定された位置から Unicode 文字のストリームを書き込むために使用するストリームを取得します。|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservernclob.md)|指定された **String** が **NCLOB** の指定された位置から書き込まれます。|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlservernclob.md)|**NCLOB** 値を指定された長さに切り捨てます。|  
  
## <a name="inherited-methods"></a>継承されたメソッド  
  
|継承元のクラス|メソッド|  
|--------------------------|-------------|  
|java.lang.Object|clone、equals、finalize、getClass、hashCode、notify、notifyAll、toString、wait|  
|java.sql.Clob|free、getAsciiStream、getCharacterStream、getSubString、length、position、setAsciiStream、setCharacterStream、setString、truncate|  
  
## <a name="see-also"></a>参照  
 [SQLServerClob クラス](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
