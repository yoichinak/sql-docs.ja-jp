---
description: setSendTimeAsDatetime メソッド (SQLServerDataSource)
title: setSendTimeAsDatetime メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 705a0494-b5e2-43db-940a-1b8cec550cdb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 52136134199ac4811d22b48bfbad768dbcdf8e7d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458408"
---
# <a name="setsendtimeasdatetime-method-sqlserverdatasource"></a>setSendTimeAsDatetime メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  このメソッドは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 で追加されました。  
  
 **sendTimeAsDatetime** 接続プロパティの設定を変更します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setSendTimeAsDatetime(boolean sendTimeAsDateTime)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sendTimeAsDateTime*  
  
 ブール値です。 true の場合、java.sql.Time 値は  の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime** 型としてサーバーに送信されます。 false の場合、java.sql.Time 値は  の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **time** 型としてサーバーに送信されます。  
  
## <a name="remarks"></a>解説  
 [SQLServerDataSource.getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md) は、**sendTimeAsDatetime** 接続プロパティの設定が返されます。  
  
 **sendTimeAsDatetime** 接続プロパティの詳細については、「[接続プロパティの設定](../../../connect/jdbc/setting-the-connection-properties.md)」を参照してください。  
  
 詳細については、「[java.sql.Time の値をサーバーに送信する方法の構成](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
