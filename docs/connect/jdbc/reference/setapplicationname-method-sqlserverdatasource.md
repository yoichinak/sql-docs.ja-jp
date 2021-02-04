---
description: setApplicationName メソッド (SQLServerDataSource)
title: setApplicationName メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerDataSource.setApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 24d6e48d-53c4-4da2-a6de-1cdff463c9cd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f49c91bcd43e926f4bdc4a604efccb5ec8ea0b92
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99174094"
---
# <a name="setapplicationname-method-sqlserverdatasource"></a>setApplicationName メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  アプリケーション名を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setApplicationName(java.lang.String applicationName)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *applicationName*  
  
 アプリケーションの名前を表す **文字列** です。  
  
## <a name="remarks"></a>解説  
 アプリケーション名は、個別のアプリケーションを識別するために、さまざまな [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] プロファイリング ツールおよびロギング ツールで使用されます。 アプリケーション名を設定しない場合は、getApplicationName メソッドによって非ローカライズ文字列 "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]" が返されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
