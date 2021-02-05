---
description: updateBinaryStream (java.lang.String, java.io.InputStream) メソッド
title: updateBinaryStream メソッド (java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 56883144-26a0-4f45-ad36-4f616369af3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9cf9c5b6047083f64dad5e029ec9f9301ef23be4
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99183284"
---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream"></a>updateBinaryStream (java.lang.String, java.io.InputStream) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された列をバイナリ ストリーム値で更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
                               java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnLabel*  
  
 列ラベルを含む **文字列** です。  
  
 *x*  
  
 InputStream オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この updateBinaryStream メソッドは、java.sql.ResultSet インターフェイスの updateBinaryStream メソッドで規定されています。  
  
 このメソッドを **image**、**text**、**ntext** の SQL Server データ型に対して使用すると、パフォーマンスに影響を及ぼす可能性があります。  
  
 このメソッドは、InputStream オブジェクトからのバイトを、binary、varbinary、varbinary(max)、image、xml、udt など、選択した [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] バイナリ列に渡します。 このメソッドでは、文字型の列の更新はサポートされていません。 InputStream で文字型の列を更新するには、[updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) メソッドを使用します。  
  
## <a name="see-also"></a>参照  
 [updateBinaryStream メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
