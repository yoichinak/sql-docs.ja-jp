---
title: 階層を含む XQueries |Microsoft Docs
description: 階層を含む XQueries の例を表示します。
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
- hierarchies [XQuery]
- XQuery, hierarchies
ms.assetid: 6953d8b7-bad8-4b64-bf7b-12fa4f10f65c
author: rothja
ms.author: jroth
ms.openlocfilehash: fdebb93459b9519eb6495054908208de610e8222
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100352797"
---
# <a name="xqueries-involving-hierarchy"></a>階層に関係する XQuery
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  **AdventureWorks** データベースのほとんどの **xml** 型の列は、半構造化されたドキュメントです。 したがって、各行に格納されているドキュメントは、外観が異なる場合があります。 このトピックのクエリサンプルでは、これらのさまざまなドキュメントから情報を抽出する方法について説明します。  
  
## <a name="examples"></a>例  
  
### <a name="a-from-the-manufacturing-instructions-documents-retrieve-work-center-locations-together-with-the-first-manufacturing-step-at-those-locations"></a>A. 製造手順ドキュメントから、ワークセンターの場所とその場所の最初の製造手順を取得します。  
 製品モデル7では、<`ManuInstr`> 要素、 **Productmodelid** 属性、 **ProductModelName** 属性、および1つ以上の <> 子要素を含む XML が構築され `Location` ます。  
  
 各 <`Location`> 要素には、独自の属性セットと1つの <`step`> 子要素があります。 この <`step`> 子要素は、ワークセンターの場所での最初の製造手順です。  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   \<ManuInstr  ProdModelID = "{sql:column("Production.ProductModel.ProductModelID") }"   
                ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
            {   
              for $wc in //AWMI:root/AWMI:Location  
              return  
                <Location>  
                 {$wc/@* }  
                 <step1> { string( ($wc//AWMI:step)[1] ) } </step1>  
                </Location>  
            }  
          </ManuInstr>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   [XQuery プロローグ](../xquery/modules-and-prologs-xquery-prolog.md)の **namespace** キーワードは、名前空間プレフィックスを定義します。 このプレフィックスは、後でクエリ本文で使用されます。  
  
-   コンテキスト切り替えトークン {) と (}) を使用して、クエリを XML 構築からクエリ評価に切り替えます。  
  
-   **Sql: column ()** は、構築される XML にリレーショナル値を含めるために使用されます。  
  
-   <の `Location`> 要素を構築する場合、$wc/@ * はすべてのワークセンターの場所の属性を取得します。  
  
-   **String ()** 関数は、<> 要素から文字列値を返し `step` ます。  
  
 結果の一部を次に示します。  
  
```xml
<ManuInstr ProdModelID="7" ProductModelName="HL Touring Frame">  
   <Location LocationID="10" SetupHours="0.5"   
            MachineHours="3" LaborHours="2.5" LotSize="100">  
     <step1>Insert aluminum sheet MS-2341 into the T-85A   
             framing tool.</step1>  
   </Location>  
   <Location LocationID="20" SetupHours="0.15"   
            MachineHours="2" LaborHours="1.75" LotSize="1">  
      <step1>Assemble all frame components following   
             blueprint 1299.</step1>  
   </Location>  
...  
</ManuInstr>   
```  
  
### <a name="b-find-all-telephone-numbers-in-the-additionalcontactinfo-column"></a>B. AdditionalContactInfo 列のすべての電話番号の検索  
 次のクエリでは、階層全体で <> 要素を検索することによって、特定の顧客の連絡先の追加の電話番号を取得し `telephoneNumber` ます。 <`telephoneNumber`> 要素は階層内のどこにでも表示できるので、クエリでは検索で子孫と自己演算子 (//) を使用します。  
  
```sql
SELECT AdditionalContactInfo.query('  
 declare namespace ci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
 declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
for $ph in /ci:AdditionalContactInfo//act:telephoneNumber  
   return  
      $ph/act:number  
') as x  
FROM  Person.Contact  
WHERE ContactID = 1  
```  
  
 結果を次に示します。  
  
```xml
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  111-111-1111  
\</act:number>  
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  112-111-1111  
\</act:number>  
```  
  
 最上位レベルの電話番号のみを取得するには (具体的には、<`telephoneNumber`> <> の子要素を取得するには、 `AdditionalContactInfo` クエリの FOR 式がに変更されます。  
  
 `for $ph in /ci:AdditionalContactInfo/act:telephoneNumber`.  
  
## <a name="see-also"></a>関連項目  
 [XQuery の基礎](../xquery/xquery-basics.md)   
 [XML 構築 &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
