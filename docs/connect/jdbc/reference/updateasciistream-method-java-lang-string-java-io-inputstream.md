---
description: updateAsciiStream (java.lang.String, java.io.InputStream) メソッド
title: updateAsciiStream (java.lang.String, java.io.InputStream) メソッド
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 747b0308-1ce6-4eba-bdfc-af29c21c18cf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5f42bda7c4938d1dc0a4ed3fad9bf446c63bad2d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88478514"
---
# <a name="updateasciistream-method-javalangstring-javaioinputstream"></a>updateAsciiStream (java.lang.String, java.io.InputStream) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された列を ASCII ストリーム値で更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateAsciiStream(java.lang.String columnLabel,  
                              java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnLabel*  
  
 列ラベルを含む**文字列**です。  
  
 *x*  
  
 InputStream オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この updateAsciiStream メソッドは、java.sql.ResultSet インターフェイスの updateAsciiStream メソッドで規定されています。  
  
 このメソッドは、ASCII 文字 (バイト) を、InputStream オブジェクトから変換可能な文字型の列へ渡します。これは、Unicode の ASCII の範囲 [0x00 - 0x7F] と、874、932、936、949、950、1250 から 1258 のコード ページです。 このメソッドは、対象となる照合順序ページへの変換を実行します。 変換できない変換先列を更新しようとすると、例外がスローされます。 バイナリ列の場合、そのままのバイトが渡されます。  
  
 このメソッドを **image**、**text**、**ntext**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のデータ型に対して使用すると、パフォーマンスに影響を及ぼす可能性があります。  
  
## <a name="see-also"></a>参照  
 [updateAsciiStream メソッド (SQLServerResultSet)](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
