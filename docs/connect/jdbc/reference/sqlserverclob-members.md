---
description: SQLServerClob のメンバー
title: SQLServerClob のメンバー | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apitype: Assembly
ms.assetid: 7db785ca-edd5-4833-8053-17fdbf87279a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c08ab28a64ddbb463f8a86d2d5a8a66f14f1ca82
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88478574"
---
# <a name="sqlserverclob-members"></a>SQLServerClob のメンバー
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  次の表は、[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md) クラスによって公開されるメンバーを示しています。  
  
## <a name="constructors"></a>コンストラクター  
  
|名前|説明|  
|----------|-----------------|  
|[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-constructor-sqlserverconnection-java-lang-string.md)|SQLServerClob クラスの新しいインスタンスを初期化します。|  
  
## <a name="fields"></a>フィールド  
 [なし] :  
  
## <a name="inherited-fields"></a>継承されたフィールド  
 [なし] :  
  
## <a name="methods"></a>メソッド  
  
|名前|説明|  
|----------|-----------------|  
|[free](../../../connect/jdbc/reference/free-method-sqlserverclob.md)|このメソッドは、CLOB オブジェクトと、それが占有していたリソースを解放します。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverclob.md)|Clob を ASCII ストリームとして具体化します。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)|Clob データを、java.io.Reader オブジェクトまたは文字のストリームとして返します。|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlserverclob.md)|渡された開始位置とコピーする文字数に基づいて、指定された Clob の部分文字列のコピーを返します。|  
|[length](../../../connect/jdbc/reference/length-method-sqlserverclob.md)|Clob の文字数を返します。|  
|[position](../../../connect/jdbc/reference/position-method-sqlserverclob.md)|指定された開始位置に基づいて、指定された Clob オブジェクトまたは Clob の部分文字列の文字位置を返します。|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlserverclob.md)|ASCII 文字を Clob の指定された位置から書き込むために使用するストリームを返します。|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverclob.md)|Unicode 文字のストリームを Clob の指定された位置から書き込むために使用するストリームを返します。|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)|渡された文字列を Clob の指定された位置から書き込みます。|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlserverclob.md)|Clob を指定された長さに切り捨てます。|  
  
## <a name="inherited-methods"></a>継承されたメソッド  
  
|継承元のクラス|メソッド|  
|--------------------------|-------------|  
|java.lang.Object|clone、equals、finalize、getClass、hashCode、notify、notifyAll、toString、wait|  
  
## <a name="see-also"></a>参照  
 [SQLServerClob クラス](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
