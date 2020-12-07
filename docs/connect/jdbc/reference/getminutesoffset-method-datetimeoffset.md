---
description: getMinutesOffset (DateTimeOffset) メソッド
title: getMinutesOffset メソッド (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a3184c0dc0389a696904386361496ea31582b0af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435414"
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
  
  
