---
description: setURL メソッド (SQLServerDataSource)
title: setURL メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea70100-ac98-4625-8748-ef7cc0b111ea
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e27df8b938cee4503a2078d597b12eb880f52c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467124"
---
# <a name="seturl-method-sqlserverdatasource"></a>setURL メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データ ソースへの接続に使用される URL を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setURL(java.lang.String url)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *url*  
  
 URL を含む**文字列**です。  
  
## <a name="remarks"></a>解説  
 セキュリティ上の理由から、setURL メソッドに渡す URL にはパスワードを含めないでください。 これは、サードパーティの Java アプリケーション サーバーでは、データ ソースの構成用ユーザー インターフェイスに、URL プロパティの値セットが表示されることが非常に多いためです。 パスワードを含める代わりに、[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) メソッドを使用してパスワード値を設定してください。 Java アプリケーション サーバーで、データ ソース内に設定されたパスワードが構成用ユーザー インターフェイスに表示されなくなります。  
  
> [!NOTE]  
>  setURL メソッドを事前に呼び出さずに [getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md) メソッドを呼び出すと、getURL は既定値の "jdbc:sqlserver://" を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
