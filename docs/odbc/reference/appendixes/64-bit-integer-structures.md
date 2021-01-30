---
description: 64 ビットの整数の構造
title: 64ビット整数構造体 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cda6c3bd7e1ad9e850d6c9bbb0c444e5bf3e5f5f
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99198164"
---
# <a name="64-bit-integer-structures"></a>64 ビットの整数の構造
Microsoft C コンパイラでの SQL_C_SBIGINT および SQL_C_UBIGINT データ型識別子の C 型は _int64 です。 Microsoft® C コンパイラ以外のコンパイラを使用する場合、C 型は異なる場合があります。 コンパイラが64ビット整数をネイティブでサポートしている場合は、ドライバーまたはアプリケーションで ODBCINT64 を定義して、ネイティブの64ビット整数型にする必要があります。 コンパイラが64ビット整数をネイティブでサポートしていない場合、アプリケーションまたはドライバーは次の構造を定義して、このデータにアクセスできるようにすることができます。  
  
```  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLUINTEGER dwHighWord;  
} SQLUBIGINT  
  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLINTEGER sdwHighWord;  
} SQLBIGINT  
```  
  
 64ビットの整数は8バイトの境界に配置されるため、これらの構造は8バイトの境界に合わせて配置する必要があります。
