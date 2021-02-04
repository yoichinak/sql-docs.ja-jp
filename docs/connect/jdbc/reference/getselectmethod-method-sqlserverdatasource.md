---
description: getSelectMethod メソッド (SQLServerDataSource)
title: getSelectMethod メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDataSource.getSelectMethod
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b6255d2e-0028-474a-afa8-553ef092243e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b7f60926fdf69a27c5e78d2817084cfe1500f91b
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99175043"
---
# <a name="getselectmethod-method-sqlserverdatasource"></a>getSelectMethod メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトを使用して作成されるすべての結果セットで使用される、既定のカーソルの種類が返されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getSelectMethod()  
```  
  
## <a name="return-value"></a>戻り値  
 既定のカーソルの種類を含む **String** 値です。  
  
## <a name="remarks"></a>解説  
 selectMethod プロパティは、結果セットで使用される既定のカーソルの種類を指定します。 このプロパティは、大きな結果セットを処理しているときに、クライアント側のメモリに結果セット全体を格納したくない場合に役立ちます。 このプロパティを "cursor" に設定することで、一度にフェッチするデータのチャンクを小さくできるサーバー側のカーソルを作成できます。 selectMethod プロパティが設定されていない場合、getSelectMethod は既定値の "direct" を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
