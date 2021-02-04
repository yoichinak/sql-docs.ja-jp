---
description: getTrustStore メソッド (SQLServerDataSource)
title: getTrustStore メソッド (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- getTrustStore Method (SQLServerDataSource)
apilocation:
- getTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 8f5850e4-8627-49a8-ba0e-b1f4014322a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 71365a85690c74025b6d807eb4def767156996cd
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99165466"
---
# <a name="gettruststore-method-sqlserverdatasource"></a>getTrustStore メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  証明書の trustStore ファイルへのパス (ファイル名を含む) を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getTrustStore()  
```  
  
## <a name="return-value"></a>戻り値  
 証明書の trustStore ファイルへのパス (ファイル名を含む) を含む **文字列** です。値が設定されていない場合は null です。  
  
## <a name="remarks"></a>解説  
 trustStore プロパティが設定されていない場合、[getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md) メソッドは null を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
