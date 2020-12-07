---
description: updateShort (int, short) メソッド
title: updateShort (int, short) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateShort (int, short)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 155b9189-cb97-4264-b42c-bbda1c7d624f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2585d0c5485b3e64f051c6bffcd867f762fd7d21
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450077"
---
# <a name="updateshort-method-int-short"></a>updateShort (int, short) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された列インデックスを使用して、指定された列を **short** 値で更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateShort(int index,  
                        short x)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *インデックス*  
  
 列インデックスを示す **int** です。  
  
 *x*  
  
 **short** 値です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この updateShort メソッドは、java.sql.ResultSet インターフェイスの updateShort メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [updateShort メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateshort-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
