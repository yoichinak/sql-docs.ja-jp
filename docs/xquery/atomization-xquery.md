---
title: アトミック化 (XQuery) |Microsoft Docs
description: 項目の型指定された値を抽出する XQuery のアトミック化プロセスについて説明します。
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, atomization
- atomization [XQuery]
ms.assetid: e3d7cf2f-c6fb-43c2-8538-4470a6375af5
author: rothja
ms.author: jroth
ms.openlocfilehash: e12ac51b38073363edf7774f4ac8046c1985b38c
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100340532"
---
# <a name="atomization-xquery"></a>アトミック化 (XQuery)
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  アトミック化とは、アイテムの型指定された値を抽出するプロセスです。 このプロセスは、特定の状況では暗黙的に実行されます。 算術演算子や比較演算子などの一部の XQuery 演算子は、このプロセスに依存します。 たとえば、算術演算子を直接ノードに適用する場合、ノードの型指定された値は、 [データ関数](../xquery/data-accessor-functions-data-xquery.md)を暗黙的に呼び出すことによって最初に取得されます。 これにより、アトミック値がオペランドとして算術演算子に渡されます。  
  
 たとえば、次のクエリは LaborHours 属性の合計を返します。 この場合、 **data ()** が属性ノードに暗黙的に適用されます。  
  
```  
declare @x xml  
set @x='<ROOT><Location LID="1" SetupTime="1.1" LaborHours="3.3" />  
<Location LID="2" SetupTime="1.0" LaborHours="5" />  
<Location LID="3" SetupTime="2.1" LaborHours="4" />  
</ROOT>'  
-- data() implicitly applied to the attribute node sequence.  
SELECT @x.query('sum(/ROOT/Location/@LaborHours)')  
```  
  
 必須ではありませんが、 **data ()** 関数を明示的に指定することもできます。  
  
```  
SELECT @x.query('sum(data(ROOT/Location/@LaborHours))')  
```  
  
 暗黙のアトミック化のもう1つの例は、算術演算子を使用する場合です。 演算子には **+** アトミック値が必要です。また、LaborHours 属性のアトミック値を取得するために、 **データ ()** が暗黙的に適用されます。 このクエリは、ProductModel テーブルの **xml** 型の命令列に対して指定されています。 次のクエリでは、LaborHours 属性が3回返されます。 クエリでは、次の点に注意してください。  
  
-   OrignialLaborHours 属性の構築では、(`$WC/@LaborHours`) によって返される単一シーケンスにアトミック化が暗黙的に適用されます。 LaborHours 属性の型指定された値は、OrignialLaborHours に割り当てられます。  
  
-   UpdatedLaborHoursV1 属性の構築では、算術演算子がアトミック値を必要とします。 そのため、() によって返される LaborHours 属性には、 **データ ()** が暗黙的に適用され `$WC/@LaborHours` ます。 次に、atomic 値1が追加されます。 属性 UpdatedLaborHoursV2 の構築には、明示的な **データ ()** の適用が示されていますが、必須ではありません。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location[1]  
        return  
            <WC OriginalLaborHours = "{ $WC/@LaborHours }"  
                UpdatedLaborHoursV1 = "{ $WC/@LaborHours + 1 }"   
                UpdatedLaborHoursV2 = "{ data($WC/@LaborHours) + 1 }" >  
            </WC>') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 結果を次に示します。  
  
```  
<WC OriginalLaborHours="2.5"   
    UpdatedLaborHoursV1="3.5"   
    UpdatedLaborHoursV2="3.5" />  
```  
  
 アトミック化を実行すると、単純型のインスタンス、空のセット、または静的な型エラーが発生します。  
  
 アトミック化は、関数に渡される比較式のパラメーター、関数によって返される値、 **cast ()** 式、および order by 句で渡される順序付け式でも発生します。  
  
## <a name="see-also"></a>参照  
 [XQuery の基礎](../xquery/xquery-basics.md)   
 [XQuery&#41;&#40;比較式 ](../xquery/comparison-expressions-xquery.md)   
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
