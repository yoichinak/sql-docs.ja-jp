---
description: SQLServerException クラス
title: SQLServerException クラス | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: af5ef257-7cf6-4db3-b1ee-07d22d82bef1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b096f1b41cc817b216cea9ff3618e7731abd5003
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450527"
---
# <a name="sqlserverexception-class"></a>SQLServerException クラス
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  SQL ステートメントの実行に失敗したこと、または実行が完了しなかったことを表します。  
  
 **パッケージ:** com.microsoft.sqlserver.jdbc  
  
 **継承:** java.sql.SQLException  
  
 **実装:** java.io.Serializable  
  
## <a name="syntax"></a>構文  
  
```  
  
public final class SQLServerException  
```  
  
## <a name="remarks"></a>解説  
 SQLServerException クラスでは、SQL 92 と XOPEN の両方の状態コードが処理されます。 これらは、ユーザー指定の接続プロパティを使用して切り替えることができます。 例外は、開いている指定のログ ファイルに書き込まれます。  
  
## <a name="see-also"></a>参照  
 [SQLServerException のメンバー](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [JDBC Driver API リファレンス](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
