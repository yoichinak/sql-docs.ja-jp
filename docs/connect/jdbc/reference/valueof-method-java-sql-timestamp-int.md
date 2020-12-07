---
description: valueOf (java.sql.Timestamp, int) メソッド
title: valueOf (java.sql.Timestamp, int) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d9797c5109b34897aca747d091949975eefc3727
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88396128"
---
# <a name="valueof-method-javasqltimestamp-int"></a>valueOf (java.sql.Timestamp, int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  引数に java.sql.Timestamp 値とオフセット (分) を示す値を受け取って、GMT からの特定のオフセットで特定の時点を表す **DateTimeOffset** オブジェクトを作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, int minutesOffset)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *timestamp*  
  
 java.sql.Timestamp値です。  
  
 *minutesOffset*  
  
 分単位のオフセットです。  
  
## <a name="return-value"></a>戻り値  
 GMT からの特定のオフセット (分) において java.sql.Timestamp オブジェクトで指定された特定の時点を表す DateTimeOffset オブジェクトを返します。  
  
## <a name="see-also"></a>参照  
 [DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset のメンバー](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
