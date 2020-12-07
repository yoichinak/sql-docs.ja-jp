---
description: executeUpdate () メソッド
title: executeUpdate メソッド () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeUpdate ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ca534c6b-ef4d-4ae8-8cc3-514728623cff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d0a973d76e44869c2eb7584bbc7127f4613a5139
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437604"
---
# <a name="executeupdate-method-"></a>executeUpdate () メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) オブジェクトの SQL ステートメントを実行します。SQL ステートメントは、SQL INSERT、UPDATE、MERGE、または DELETE ステートメントであるか、DDL ステートメントなどのような何も返さない SQL ステートメントであることが必要です。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int executeUpdate()  
```  
  
## <a name="return-value"></a>戻り値  
 影響を受けた行数を示す **int** です。DDL ステートメントを使用している場合は 0 です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この executeUpdate メソッドは、java.sql.PreparedStatement インターフェイスの executeUpdate メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [executeUpdate メソッド &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement のメンバー](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement クラス](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
