---
description: updateCharacterStream (int, java.io.Reader) メソッド
title: updateCharacterStream (int, java.io.Reader) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4dddf885-0482-4776-8e9a-69f6c6270931
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8f4d8d4ae626fada30b9dacda009ddfe5a2553fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88354018"
---
# <a name="updatecharacterstream-method-int-javaioreader"></a>updateCharacterStream (int, java.io.Reader) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された列を文字ストリームの値で更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateCharacterStream(int columnIndex,  
                                  java.io.Reader x)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnIndex*  
  
 列インデックスを示す **int** です。  
  
 *x*  
  
 Reader オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この updateCharacterStream メソッドは、java.sql.ResultSet インターフェイスの updateCharacterStream メソッドで規定されています。  
  
 このメソッドは、Unicode 文字を Reader オブジェクトから選択したテキストおよびバイナリ列に渡します。 これには、すべてのテキスト列と **binary**、**varbinary**、**varbinary(max)** 、**image**、**xml** の各列が含まれますが、**udt** 列は含まれません。  
  
 このメソッドを **image**、**text**、**ntext**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のデータ型に対して使用すると、パフォーマンスに影響を及ぼす可能性があります。  
  
## <a name="see-also"></a>参照  
 [updateCharacterStream メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
