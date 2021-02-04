---
description: getFailoverPartner メソッド (SQLServerDataSource)
title: getFailoverPartner メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDataSource.getFailoverPartner
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 885f927f-9c48-42e0-a7fb-fd936d2b8130
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b5084e93cbe03ef79e5858757bf8b627991d9902
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99163057"
---
# <a name="getfailoverpartner-method-sqlserverdatasource"></a>getFailoverPartner メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベース ミラーリング構成で使用されるフェールオーバー サーバーの名前を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public string getFailoverPartner()  
```  
  
## <a name="return-value"></a>戻り値  
 フェールオーバー パートナーの名前を含む **文字列** です。何も設定されていない場合は null です。  
  
## <a name="remarks"></a>解説  
 このメソッドによって返された値は、[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) メソッドを使用して設定されたフェールオーバー パートナー名を反映しています。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
