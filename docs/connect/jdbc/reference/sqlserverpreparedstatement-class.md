---
description: SQLServerPreparedStatement クラス
title: SQLServerPreparedStatement クラス | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8481c06-fbba-432b-8c69-4f4619c20ad4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 75a04a0873308cc09c16b54f5d482ed54a20c0b1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472144"
---
# <a name="sqlserverpreparedstatement-class"></a>SQLServerPreparedStatement クラス
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC の準備されたステートメント機能の基本的な実装を表します。  
  
 **パッケージ:** com.microsoft.sqlserver.jdbc  
  
 **継承:** SQLServerStatement  
  
 **実装:** [ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
public class SQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>解説  
 SQLServerPreparedStatement は、任意の Java ネイティブ型および多数の Java オブジェクト型としてパラメーターを指定できるメソッドを提供します。 SQLServerPreparedStatement では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **sp_prepare** ストアド プロシージャを使用してステートメントが準備され、それ以降のそのステートメントの実行は、返されたステートメント ハンドルを再利用し、通常はユーザーが提供するさまざまなパラメーターを使用して行われます。  
  
 SQLServerPreparedStatement ではバッチ処理がサポートされており、準備されたステートメントのセットが単一のデータベースのラウンド トリップで実行され、実行時パフォーマンスが向上します。  
  
 このクラスでは、SQLServerPreparedStatement クラス、ISQLServerPreparedStatement インターフェイス、java.sql.PreparedStatement インターフェイス、および SQLServerStatement によってラップ解除がサポートされているクラスとインターフェイスへのラップ解除がサポートされます。 詳細については、「[ラッパーとインターフェイス](../../../connect/jdbc/wrappers-and-interfaces.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLServerPreparedStatement のメンバー](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [JDBC Driver API リファレンス](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
