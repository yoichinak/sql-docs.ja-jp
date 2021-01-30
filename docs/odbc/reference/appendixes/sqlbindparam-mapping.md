---
description: SQLBindParam のマッピング
title: SQLBindParam Mapping |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- SQLBindparam function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLBindParam
ms.assetid: 375f8f24-36de-4946-916e-c75abc6f070d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62951dc5ae69e86eb5cbc2fba21407d63952e74b
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202933"
---
# <a name="sqlbindparam-mapping"></a>SQLBindParam のマッピング
**SQLBindParam** は ODBC に存在しないため、実際には非推奨として呼び出すことはできません。ただし、これは重複した機能を表しています。 ISO とオープングループに準拠しているアプリケーションで使用されるため、ドライバーマネージャーはこれをエクスポートする必要があります。 **SQLBindParameter** には **SQLBindParam** のすべての機能が含まれているため、 **SQLBindParam** は **SQLBindParameter** の上にマップされます (基になるドライバー *が ODBC 3.x* ドライバーの場合)。 ODBC 3.x *ドライバーで* は、 **SQLBindParam** を実装する必要はありません。  
  
## <a name="remarks"></a>コメント  
 **SQLBindParam** を呼び出すと、次のようになります。  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 ドライバーマネージャーは、次のようにドライバーで **SQLBindParameter** を呼び出します。  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 アプリケーションが64ビットのオペレーティングシステムで実行される場合は、「 [ODBC 64 ビット情報](../../../odbc/reference/odbc-64-bit-information.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [非推奨の関数のマッピング](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
