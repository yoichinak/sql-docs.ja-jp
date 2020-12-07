---
description: 各国語文字セットのサポート
title: 各国語文字セットのサポート | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4fceacfd-df4f-40cd-b7a2-5e5e58a5979f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 394d81f28921bfc4e68204778ed6fcdf1e2fb9e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438344"
---
# <a name="national-character-set-support"></a>各国語文字セットのサポート
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  JDBC ドライバーは JDBC 4.0 API をサポートし、新しく各国語文字セットの変換 API メソッドが追加されています。 このサポートには、**NCHAR**、**NVARCHAR**、**LONGNVARCHAR**、**NCLOB** JDBC 型の新しい setter メソッド、getter メソッド、updater メソッドが含まれています。  
  
 以下は、各国語文字セットの変換をサポートする新しい getter、setter、および updater メソッドの一覧です。  
  
-   [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md): [setNString](../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md)、[setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)、[setNClob](../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)。  
  
-   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)、[getNString](../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)、[getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)、[setNString](../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md)、[setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)、[setNClob](../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)。  
  
-   [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)、[getNString](../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)、[getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)、[updateNClob](../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)、[updateNString](../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)、[updateNCharacterStream](../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)。  
  
> [!NOTE]  
>  アプリケーション内でこれらのメソッドを使用するには、sqljdbc4.jar ファイルをインクルードするためのクラスパスを設定する必要があります。  
  
 アプリケーションからサーバーに対し文字列パラメーターを Unicode 形式で送信するには、JDBC 4.0 の新しい National Character メソッドを使用する必要があります。National Character メソッド以外のメソッドを使用する場合は、**sendStringParametersAsUnicode** 接続プロパティを "**true**" に設定する必要があります。 できる限り、JDBC 4.0 の新しい National Character メソッドを使用することをお勧めします。 **sendStringParametersAsUnicode** 接続プロパティについて詳しくは、「[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目  
 [JDBC ドライバーのデータ型について](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
