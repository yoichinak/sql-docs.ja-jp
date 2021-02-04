---
description: getNClob (int) メソッド
title: getNClob メソッド (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 10dfa251-9408-469e-ae2a-1acf3917cf47
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4cfd906b2b109d2785c016e82971f289622c1bec
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99175401"
---
# <a name="getnclob-method-int"></a>getNClob (int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された JDBC **NCLOB** パラメーターの値を Java プログラミング言語の NClob オブジェクトとして取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.NClob getNClob(int parameterIndex)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *parameterIndex*  
  
 パラメーターのインデックスを示す **int** です。  
  
## <a name="return-value"></a>戻り値  
 NClob オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getNClob メソッドは、java.sql.CallableStatement インターフェイスの getNClob メソッドで規定されています。  
  
 このメソッドは、**NCHAR**、**NVARCHAR**、**NTEXT**、**XML** パラメーターの取得のみをサポートしています。 これらのメソッドを他のデータ型のパラメーターで呼び出すと、例外が発生します。  
  
## <a name="see-also"></a>参照  
 [getNClob メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
