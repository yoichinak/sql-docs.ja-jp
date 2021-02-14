---
title: max 関数 (XQuery) |Microsoft Docs
description: 値が他のすべての項目よりも大きいシーケンス内の1つの項目を返す XQuery max () 関数について説明します。
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- max function [XQuery]
- fn:max function
ms.assetid: 5ee625c0-044a-4cda-b210-02b64e619d65
author: rothja
ms.author: jroth
ms.openlocfilehash: b52ae499cf09e8fcd024f592ae639d0f9a7c1c5a
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100341960"
---
# <a name="aggregate-functions---max"></a>集計関数 - max
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  アトミック値のシーケンス ( *$arg*) から、その値が他の値より大きい値を持つ1つの項目を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:max($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 最大値の取得元となるアトミック値のシーケンス。  
  
## <a name="remarks"></a>Remarks  
 **Max ()** に渡されるアトミック値のすべての型は、同じ基本型のサブタイプである必要があります。 許容される基本型は、 **gt** 操作をサポートする型です。 これらの型には、3つの組み込み数値基本型、日付/時刻の基本型、xs: string、xs: boolean、および xdt: untypedAtomic が含まれます。 Xdt: untypedAtomic 型の値は、xs: double にキャストされます。 これらの型が混在している場合、または他の型の他の値が渡された場合は、静的エラーが発生します。  
  
 Xdt: untypedAtomic の場合、 **max ()** の結果は、xs: double など、渡された型の基本型を受け取ります。 入力が静的に空の場合、空のが暗黙的に指定され、静的なエラーが発生します。  
  
 **Max ()** 関数は、入力シーケンス内の他の値よりも大きいシーケンス内の1つの値を返します。 Xs: string 値の場合、既定の Unicode コードポイント照合順序が使用されます。 Xdt: untypedAtomic 値を xs: double にキャストできない場合、入力シーケンスの値は無視されます ( *$arg*)。 入力が動的に計算された空のシーケンスである場合は、空のシーケンスが返されます。  
  
## <a name="examples"></a>使用例  
 このトピックでは、データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示し [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] ます。  
  
### <a name="a-using-the-max-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-that-have-the-most-labor-hours"></a>A. Max () XQuery 関数を使用して、製造プロセス内で最も労働時間があるワークセンターの場所を検索する  
 [Min 関数 (XQuery)](../xquery/aggregate-functions-min.md)で指定されたクエリは、 **max ()** 関数を使用するように書き直すことができます。  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   **Max (**) 関数では、すべての整数が xs: decimal にマップされます。  
  
-   Xs: duration 型の値に対する **max ()** 関数はサポートされていません。  
  
-   基本データ型の境界を超えて複数の型が混在するシーケンスはサポートされません。  
  
-   照合順序を提供する構文オプションはサポートされていません。  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
