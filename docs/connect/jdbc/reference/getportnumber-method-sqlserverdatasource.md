---
description: getPortNumber メソッド (SQLServerDataSource)
title: getPortNumber メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ded903bb6696c3dfefd51979d37605af899b6d6d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435014"
---
# <a name="getportnumber-method-sqlserverdatasource"></a>getPortNumber メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] との通信に使用される現在のポート番号が返されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>戻り値  
 現在のポート番号を含む **int** 値です。  
  
## <a name="remarks"></a>解説  
 このポート番号は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] へのソケット接続を開くときに使用される TCP/IP ポート番号です。 portNumber プロパティが設定されていない場合、getPortNumber メソッドは既定値の 1433 を返します。  
  
> [!NOTE]  
>  [setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md) メソッドでは、渡されたポート値に対する範囲チェックは行われません。 エラーをトリガーすることなく、99999 のように無効なポート番号を渡すことができます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
