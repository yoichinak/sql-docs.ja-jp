---
description: setXopenStates メソッド (SQLServerDataSource)
title: setXopenStates メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDataSource.setXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9723591f-e987-426f-b70a-07f5c70dc094
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ea389a352ec117e6cd59acf709bb6300434d5cf
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99178428"
---
# <a name="setxopenstates-method-sqlserverdatasource"></a>setXopenStates メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  XOPEN 互換の状態への SQL 状態の変換が有効になっているかどうかを示す **Boolean** 値を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setXopenStates(boolean xopenStates)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *xopenStates*  
  
 XOPEN 互換の状態への SQL 状態の変換が有効になっている場合は **true** です。 それ以外の場合は、 **false** です。  
  
## <a name="remarks"></a>解説  
 xopenStates プロパティが **true** に設定されている場合、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] は SQL 状態を XOPEN 互換の状態に変換します。 既定値は **false** です。この場合、JDBC ドライバーは SQL 99 の状態コードを生成します。 xopenStates が設定されていない場合、[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md) メソッドは既定値の **false** を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
