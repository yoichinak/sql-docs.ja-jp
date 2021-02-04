---
description: setEscapeProcessing メソッド (SQLServerStatement)
title: setEscapeProcessing メソッド (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerStatement.setEscapeProcessing
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6ac0682e-e04c-4fdb-893b-92408d42051e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c60d547ed0a72a573bda8f16b4051ff796261dd5
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99173457"
---
# <a name="setescapeprocessing-method-sqlserverstatement"></a>setEscapeProcessing メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  エスケープの処理モードを設定します。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] では、エスケープ処理が常に有効になっています。 このメソッドを false に設定しても効果はありません。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setEscapeProcessing(boolean enable)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *enable*  
  
 エスケープ処理を有効にする場合は **true** です。 それ以外の場合は、 **false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setEscapeProcessing メソッドは、java.sql.Statement インターフェイスの setEscapeProcessing メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
