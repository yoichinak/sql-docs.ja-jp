---
title: 算術式 (XQuery) |Microsoft Docs
description: XQuery の算術式とサポートされる算術演算子について説明します。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
author: rothja
ms.author: jroth
ms.openlocfilehash: f63fd1f6064d28a7ee977162e8993f53f9233519
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100340487"
---
# <a name="arithmetic-expressions-xquery"></a>算術式 (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  **Idiv** を除き、すべての算術演算子がサポートされています。 次の例は、算術演算子の基本的な使用方法を示しています。  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 **Idiv** はサポートされていないため、ソリューションでは **xs: integer ()** コンストラクターを使用します。  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 算術演算子の結果の型は、入力値の型に基づいています。 オペランドどうしの型が異なる場合、必要に応じて一方または両方のオペランドが、データ型階層に基づき共通のプリミティブな基本データ型にキャストされます。 型階層の詳細については、「 [XQuery での型キャストの規則](../xquery/type-casting-rules-in-xquery.md)」を参照してください。  
  
 数値データ型の上位変換は、2 つのオペランドが異なる数値基本データ型である場合に行われます。 たとえば、xs: **decimal** を **xs: double** に追加すると、最初に10進値が double に変更されます。 次に、加算を実行して、倍精度浮動小数点型の値を生成します。  
  
 型指定されていないアトミック値は、もう一方のオペランドの数値基本型にキャストされるか、もう一方のオペランドも型指定されていない場合は **xs: double** にキャストされます。  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   算術演算子の引数は、数値型または **untypedAtomic** である必要があります。  
  
-   **Xs: integer** 値に対する操作では、 **xs: integer** ではなく **xs: decimal** 型の値が返されます。  
  
  
