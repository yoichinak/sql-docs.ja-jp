---
description: getMinutesOffset (DateTimeOffset) メソッド
title: getMinutesOffset メソッド (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44fe6c4be49cc8896ee1f59e3794617e839d8744
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99175466"
---
# <a name="getminutesoffset-method-datetimeoffset"></a>getMinutesOffset (DateTimeOffset) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  この DateTimeOffset オブジェクトの GMT からのオフセット (分単位) を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>戻り値  
 分単位のオフセットです。  
  
## <a name="remarks"></a>解説  
 2010 年 3 月 8 日 11:35:48 -0800 を表す DateTimeOffset オブジェクトの場合、getMinutesOffset は 480 の値を返します。  
  
## <a name="see-also"></a>参照  
 [DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset のメンバー](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
