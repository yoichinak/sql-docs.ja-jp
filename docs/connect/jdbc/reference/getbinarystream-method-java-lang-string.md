---
description: getBinaryStream (java.lang.String) メソッド
title: getBinaryStream メソッド (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBinaryStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 149609b5-a6de-4e23-a440-7061775d0899
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d0887b6cd8770310304596606ace6bba321465c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437254"
---
# <a name="getbinarystream-method-javalangstring"></a>getBinaryStream (java.lang.String) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列名の値を、未解釈のバイトのバイナリ ストリームとして取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.io.InputStream getBinaryStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnName*  
  
 列名を含む**文字列**です。  
  
## <a name="return-value"></a>戻り値  
 InputStream オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getBinaryStream メソッドは、java.sql.ResultSet インターフェイスの getBinaryStream メソッドで規定されています。  
  
 このメソッドを使用できる [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型は、binary、varbinary、varbinary(max)、および image だけです。 他のデータ型で使用すると、例外がスローされます。  
  
 このメソッドで値をストリームとして取得した後は、ストリームからこの値をチャンク単位で読み取ることができます。 このメソッドは、大きな LONGVARBINARY 値を取得する場合に適しています。  
  
> [!NOTE]  
>  返されたストリーム内のデータはすべて、他の列の値を取得する前に読み取る必要があります。 次に getter メソッドを呼び出すと、ストリームは暗黙的に閉じます。 また、メソッド InputStream.available を呼び出した場合、使用可能なデータがあるかどうかにかかわらず、ストリームから 0 が返される可能性があります。  
  
## <a name="see-also"></a>参照  
 [getBinaryStream メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
