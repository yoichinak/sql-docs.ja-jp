---
description: getWorkstationID メソッド (SQLServerDataSource)
title: getWorkstationID メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getWorkstationID
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6a701de-a8fa-4668-9310-99a8c6e32c88
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44ba105413506ed95e5417e4a5f8b231aca19784
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433764"
---
# <a name="getworkstationid-method-sqlserverdatasource"></a>getWorkstationID メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データ ソースへの接続に使用されるクライアント コンピューターの名前を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getWorkstationID()  
```  
  
## <a name="return-value"></a>戻り値  
 クライアント コンピューターの名前を含む **String** です。  
  
## <a name="remarks"></a>解説  
 workstationID は、クライアント コンピューターまたはワークステーションの名前です。 workstationID プロパティが設定されていない場合、既定値は InetAddress.getLocalHost().getHostName() メソッドを呼び出して構成されます。 getHostName によって空白の値が返された場合は、getHostAddress().toString() メソッドが呼び出されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
