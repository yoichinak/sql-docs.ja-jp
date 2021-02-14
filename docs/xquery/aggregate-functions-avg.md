---
title: avg 関数 (XQuery) |Microsoft Docs
description: 指定された一連の数値の平均を返す XQuery 関数 avg () について説明します。
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:avg function
- avg function [XQuery]
ms.assetid: 0cc60267-3c56-4a88-8ad7-bb07f0255d56
author: rothja
ms.author: jroth
ms.openlocfilehash: ee09ab89e1acb0fc8ddad23d002e2cd0e136bc59
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100340497"
---
# <a name="aggregate-functions---avg"></a>集計関数 - avg
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  一連の数値の平均値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:avg($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 平均が計算されるアトミック値のシーケンス。  
  
## <a name="remarks"></a>Remarks  
 **Avg ()** に渡されるアトミック値のすべての型は、3つの組み込み数値基本型または xdt: untypedAtomic のいずれか1つのサブタイプである必要があります。 これらの型を混在させることはできません。 xdt:untypedAtomic 型の値は、xs:double として扱われます。 **Avg ()** の結果は、xdt: untypedAtomic の場合、xs: double など、渡された型の基本型を受け取ります。  
  
 入力が静的に空の場合、空のが暗黙的に指定され、静的なエラーが発生します。  
  
 **Avg ()** 関数は、計算された数値の平均を返します。 次に例を示します。  
  
 **sum (** *$arg* **) div count (** *$arg* **)**  
  
 *$Arg* が空のシーケンスの場合は、空のシーケンスが返されます。  
  
 Xdt: untypedAtomic 値を xs: double にキャストできない場合、入力シーケンスの値は無視されます ( *$arg*)。  
  
 他のすべての場合は、関数から静的エラーが返されます。  
  
## <a name="examples"></a>使用例  
 このトピックでは、AdventureWorks データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-using-the-avg-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-in-which-labor-hours-are-greater-than-the-average-for-all-work-center-locations"></a>A. Avg () XQuery 関数を使用して、製造プロセス内のワークセンターの場所を検索します。この場合、労働時間はすべてのワークセンターの場所の平均よりも大きくなります。  
 [Min 関数 (XQuery)](../xquery/aggregate-functions-min.md)で指定されたクエリを書き直して、 **avg ()** 関数を使用することができます。  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   **Avg ()** 関数では、すべての整数が xs: decimal にマップされます。  
  
-   Xs: duration 型の値に対する **avg ()** 関数はサポートされていません。  
  
-   基本データ型の境界を超えて複数の型が混在するシーケンスはサポートされません。  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
