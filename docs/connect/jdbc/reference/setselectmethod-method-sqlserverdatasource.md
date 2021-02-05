---
description: setSelectMethod メソッド (SQLServerDataSource)
title: setSelectMethod メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDataSource.setSelectMethod
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7934276d-5ac9-4cbc-a2a0-2c65c93733ac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8f31db4197a0d2b714bb1e1889648d24ca5a4fc3
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99178652"
---
# <a name="setselectmethod-method-sqlserverdatasource"></a>setSelectMethod メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトを使用して作成されるすべての結果セットで使用される、既定のカーソルの種類を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setSelectMethod(java.lang.String selectMethod)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *selectMethod*  
  
 既定のカーソルの種類を含む **String** 値です。  
  
## <a name="remarks"></a>解説  
 selectMethod は、結果セットで使用される既定のカーソルの種類です。 このプロパティは、大きな結果セットを処理しているときに、クライアント側のメモリに結果セット全体を格納したくない場合に役立ちます。 このプロパティを "cursor" に設定することで、一度にフェッチするデータのチャンクを小さくできるサーバー側のカーソルを作成できます。 selectMethod プロパティが設定されていない場合、[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md) は既定値の "direct" を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
