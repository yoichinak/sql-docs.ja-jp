---
title: distinct values 関数 (XQuery) |Microsoft Docs
description: XQuery で distinct values 関数を使用して、重複する値をシーケンスから削除する方法について説明します。
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
- distinct-values function
- fn:distinct-values function
ms.assetid: f4c2bb53-2bec-4f1a-9c00-cf997fb7ae5b
author: rothja
ms.author: jroth
ms.openlocfilehash: b9a3561c25ca0c64e01c2603b64656320d499518
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100341904"
---
# <a name="functions-on-sequences---distinct-values"></a>シーケンスの関数 - distinct-values
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  *$Arg* によって指定されたシーケンスから重複する値を削除します。 *$Arg* が空のシーケンスの場合、関数は空のシーケンスを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:distinct-values($arg as xdt:anyAtomicType*) as xdt:anyAtomicType*  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 アトミック値のシーケンス。  
  
## <a name="remarks"></a>Remarks  
 **個別の値 ()** に渡されるアトミック値のすべての型は、同じ基本型のサブタイプである必要があります。 許容される基本型は、 **eq** 操作をサポートする型です。 これらの型には、3つの組み込み数値基本型、日付/時刻の基本型、xs: string、xs: boolean、および xdt: untypedAtomic が含まれます。 Xdt: untypedAtomic 型の値は、xs: string にキャストされます。 これらの型が混在している場合、または他の型の他の値が渡された場合は、静的エラーが発生します。  
  
 **個別の値 ()** の結果は、渡された型の基本型 (Xdt: untypedAtomic の場合は xs: string など) を元のカーディナリティと共に受け取ります。 入力が静的に空の場合、空のが暗黙的に指定され、静的なエラーが発生します。  
  
 Xs: string 型の値は、XQuery の既定の Unicode コードポイント照合順序と比較されます。  
  
## <a name="examples"></a>使用例  
 このトピックでは、AdventureWorks データベースのさまざまな **xml** 型の列に格納されている xml インスタンスに対して XQuery の例を示します。  
  
### <a name="a-using-the-distinct-values-function-to-remove-duplicate-values-from-the-sequence"></a>A. Distinct-values () 関数を使用して、シーケンスから重複する値を削除する  
 この例では、電話番号を含む XML インスタンスが **xml** 型の変数に割り当てられています。 この変数に対して指定された XQuery は、 **distinct-values ()** 関数を使用して、重複が含まれていない電話番号のリストをコンパイルします。  
  
```  
declare @x xml  
set @x = '<PhoneNumbers>  
 <Number>111-111-1111</Number>  
 <Number>111-111-1111</Number>  
 <Number>222-222-2222</Number>  
</PhoneNumbers>'  
-- 1st select  
select @x.query('  
  distinct-values( data(/PhoneNumbers/Number) )  
') as result  
```  
  
 結果を次に示します。  
  
```  
111-111-1111 222-222-2222    
```  
  
 次のクエリでは、一連の数値 (1, 1, 2) が **個別の値 ()** 関数に渡されます。 関数は、シーケンス内の重複する値を削除し、結果として得られた 2 つの値を返します。  
  
```  
declare @x xml  
set @x = ''  
select @x.query('  
  distinct-values((1, 1, 2))  
') as result  
```  
  
 このクエリは 1 2 を返します。  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   **Distinct-values ()** 関数は、整数値を xs: decimal にマップします。  
  
-   **Distinct-values ()** 関数は、前述の型のみをサポートし、基本型の組み合わせをサポートしていません。  
  
-   Xs: duration 値に対する **distinct values ()** 関数はサポートされていません。  
  
-   照合順序を提供する構文オプションはサポートされていません。  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
