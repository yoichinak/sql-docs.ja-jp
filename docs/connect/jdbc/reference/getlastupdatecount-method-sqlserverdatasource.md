---
description: getLastUpdateCount メソッド (SQLServerDataSource)
title: getLastUpdateCount メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDataSource.getLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c4fbb24-0b02-42da-928c-a903bb591cc7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf2a9772d3fd6c97b9416e810ec3d5680ad3f559
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99162900"
---
# <a name="getlastupdatecount-method-sqlserverdatasource"></a>getLastUpdateCount メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  lastUpdateCount プロパティが有効であるかどうかを示す **Boolean** 値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean getLastUpdateCount()  
```  
  
## <a name="return-value"></a>戻り値  
 lastUpdateCount が有効な場合は **true** です。 それ以外の場合は、 **false** です。  
  
## <a name="remarks"></a>解説  
 lastUpdateCount プロパティが **true** に設定されている場合、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] は、サーバーに渡された SQL ステートメントから最終的な更新数のみを返します。 lastUpdateCount プロパティが **false** に設定されている場合、ドライバーは、発生した可能性があるすべてのトリガーが返した更新数を含む、すべての更新数を返します。 lastUpdateCount プロパティが設定されていない場合、getLastUpdateCount メソッドは既定値の **true** を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
