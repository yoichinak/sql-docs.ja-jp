---
description: updateNCharacterStream (java.lang.String, java.io.Reader, long) メソッド
title: updateNCharacterStream メソッド (String - Reader - long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: db0a96a8-248f-4664-9c13-f480f309ab91
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d72c1356f075170913179ed8c2e06ea2d060e967
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99193328"
---
# <a name="updatencharacterstream-method-javalangstring-javaioreader-long"></a>updateNCharacterStream (java.lang.String, java.io.Reader, long) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された列を文字ストリームの値で更新します。文字ストリームの値は、指定されたバイト数を持ちます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateNCharacterStream(java.lang.String columnLabel,  
                                    java.io.Reader reader,  
                                    long length)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnLabel*  
  
 列ラベルを含む **文字列** です。  
  
 *reader*  
  
 Reader オブジェクト。  
  
 *length*  
  
 ストリームの長さです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この updateNCharacterStream メソッドは、java.sql.ResultSet インターフェイスの updateNCharacterStream メソッドで指定されています。  
  
 このメソッドは、Unicode 文字を Reader オブジェクトから選択した **nchar** 列、**nvarchar(max)** 列、**ntext** 列、**xml** 列に渡します。 このメソッドを他のデータ型の列で使用すると、例外がスローされます。  
  
 ストリームの長さが、*length* パラメーターで指定された長さと異なる場合は、行の更新または挿入時に JDBC ドライバーが例外をスローします。  
  
 ストリームの長さが不明である場合、*length* パラメーターを -1 に設定して、ドライバーが長さに関係なくストリームを受け入れるように指定できます。 sqljdbc4.jar を使用する場合、アプリケーションで長さが不明なストリームを使用して列を更新するときには、JDBC 4.0 メソッドの [updateNCharacterStream メソッド &#40;java.lang.String, java.io.Reader&#41;](../../../connect/jdbc/reference/updatencharacterstream-method-java-lang-string-java-io-reader.md) を使用することをお勧めします。  
  
## <a name="see-also"></a>参照  
 [updateNCharacterStream メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
