---
description: setLastUpdateCount メソッド (SQLServerDataSource)
title: setLastUpdateCount メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDataSource.setLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5487631a-1107-4169-84ca-b77fd09bea66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dc4cc7f66e75ce6c3f69a65ab9ab71e3f4769212
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99173405"
---
# <a name="setlastupdatecount-method-sqlserverdatasource"></a>setLastUpdateCount メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  lastUpdateCount プロパティが有効であるかどうかを示す **Boolean** 値を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setLastUpdateCount(boolean lastUpdateCount)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *lastUpdateCount*  
  
 lastUpdateCount が有効な場合は **true** です。 それ以外の場合は、 **false** です。  
  
## <a name="remarks"></a>解説  
 lastUpdateCount プロパティが **true** に設定されている場合、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] は、サーバーに渡された SQL ステートメントから最終的な更新数のみを返します。 lastUpdateCount プロパティが **false** に設定されている場合、ドライバーは、発生した可能性があるすべてのトリガーが返した更新数を含む、すべての更新数を返します。 lastUpdateCount プロパティが設定されていない場合、[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md) メソッドは既定値の **true** を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
