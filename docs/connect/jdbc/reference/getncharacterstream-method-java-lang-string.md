---
description: getNCharacterStream (java.lang.String) メソッド
title: getNCharacterStream メソッド (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 45d2695b-0727-419d-8921-a51d6feef0aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7fbf13e4757ccf709d6b6d3151b454bc87b037a3
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99175424"
---
# <a name="getncharacterstream-method-javalangstring"></a>getNCharacterStream (java.lang.String) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  パラメーターに渡された名前を使用して、指定されたパラメーターの値を Reader オブジェクトとして取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnLabel*  
  
 列ラベルを含む **文字列** です。  
  
## <a name="return-value"></a>戻り値  
 Reader オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 このメソッドは、**NCHAR**、**NVARCHAR**、**LONGNVARCHAR** パラメーターにアクセスするときに使用する必要があります。  
  
 この getNCharacterStream メソッドは、java.sql.CallableStatement インターフェイスの getNCharacterStream メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [getNCharacterStream メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
