---
description: getSubString メソッド (SQLServerNClob)
title: getSubString メソッド (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 1d91c930-1bac-4da9-b9a5-ac2cfd31541b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 868bc1234c1f8f23b11b47967e5ae0d070191ccd
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99174908"
---
# <a name="getsubstring-method-sqlservernclob"></a>getSubString メソッド (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された開始位置とコピーする文字数に基づいて、指定された **NCLOB** の部分文字列のコピーを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getSubString(long pos,  
                                  int length)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *pos*  
  
 抽出する部分文字列の先頭の文字です。 先頭の文字の位置は 1 です。  
  
 *length*  
  
 コピーする連続した文字の文字数です。  
  
## <a name="return-value"></a>戻り値  
 **NCLOB** の指定された substring である **文字列** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getSubString メソッドは、java.sql.NClob インターフェイスの getSubString メソッドで規定されています。  
  
 null または長さが 0 の NCLOB から 0 文字を取得しようとすると、空の文字列が返されます。 長さが 0 の NCLOB で、位置 1 以外の場所で任意の長さの文字を取得しようとすると、位置の例外がスローされます。  
  
## <a name="see-also"></a>参照  
 [SQLServerNClob のメソッド](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob のメンバー](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob クラス](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
