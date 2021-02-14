---
title: XQuery | の型キャスト規則Microsoft Docs
description: XQuery で、あるデータ型から別のデータ型への明示的または暗黙的なキャストを行うときに適用される規則について説明します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, type casting
- casting rules [XML in SQL Server]
- explicit casting [SQL Server]
- type casting rules [XML in SQL Server]
- cast as operator
- implicit casting
ms.assetid: f2e91306-2b1b-4e1c-b6d8-a34fb9980057
author: rothja
ms.author: jroth
ms.openlocfilehash: 0cd4a68b21ae23b60c2bea5618308c0d13300cab
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100353277"
---
# <a name="type-casting-rules-in-xquery"></a>XQuery での型キャストの規則
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  次の W3C XQuery 1.0 and XPath 2.0 Functions and Operators 仕様の図は、組み込みのデータ型を示しています。 これには、組み込みのプリミティブ型と組み込みの派生型が含まれます。  
  
 ![XQuery 1.0 型の階層](../xquery/media/xquery-typing-rules.gif "XQuery 1.0 型の階層")  
  
 このトピックでは、次のいずれかの方法を使用して、ある型から別の型にキャストするときに適用される型キャストの規則について説明します。  
  
-   **Cast をとしてキャスト** するか、型コンストラクター関数 (など) を使用して明示的にキャストし `xs:integer("5")` ます。  
  
-   型の上位変換中に行われる暗黙のキャスト  
  
## <a name="explicit-casting"></a>明示的なキャスト  
 次の表は、組み込みのプリミティブ型間で許可される型キャストの概要を示しています。  
  
 ![XQuery のキャスト規則の説明](../xquery/media/casting-builtin-types.gif "XQuery のキャスト規則の説明")  
  
-   組み込みのプリミティブ型は、テーブル内の規則に基づいて、別の組み込みプリミティブ型にキャストできます。  
  
-   プリミティブ型は、そのプリミティブ型から派生した任意の型にキャストできます。 たとえば、 **xs: decimal** から **xs: integer**、または **xs: decimal** から **xs: long** にキャストできます。  
  
-   派生型は、型階層内の先祖である任意の型にキャストできます。これは、組み込みのプリミティブ基本型までのすべての方法になります。 たとえば、 **xs: token** から **Xs: normalizedstring** または **xs: string** にキャストできます。  
  
-   ある派生型は、その先祖のプリミティブ型からキャストできる型であれば、任意のプリミティブ型にキャストできます。 たとえば、派生型の xs: **integer** を **xs: string** にキャストできます。これは、xs: **decimal**、 **xs: integer** のプリミティブな先祖を **xs: string** にキャストできるためです。  
  
-   ある派生型は、その先祖のプリミティブ型からキャストできるプリミティブ型の先祖であれば、任意の派生型にキャストできます。 たとえば、xs: **decimal** から xs: **string** にキャストできるため、xs **: integer** から **xs: token** にキャストできます。  
  
-   ユーザー定義型から組み込み型にキャストする場合の規則は、組み込み型の規則と同じです。 たとえば、 **xs: integer** 型から派生した **myinteger** 型を定義できます。 次に、xs: **decimal** を xs: **string** にキャストできるため、 **myinteger** を **xs: token** にキャストできます。  
  
 次の種類のキャストはサポートされていません。  
  
-   リスト型間のキャストは許可されません。 これには、ユーザー定義リスト型と、 **xs: IDREFS**、 **xs: ENTITIES**、 **xs: NMTOKENS** などの組み込みリスト型の両方が含まれます。  
  
-   **Xs: QName** との間のキャストはサポートされていません。  
  
-   **xs: NOTATION** と、duration、 **Xdt: yearMonthDuration** 、および **xdt: daytimeduration** の完全に並べ替えられたサブタイプはサポートされていません。 したがって、これらの型間のキャストはサポートされません。  
  
 次の例は、明示的な型キャストを示しています。  
  
### <a name="example-a"></a>例 A  
 次の例では、xml 型の変数に対してクエリを行います。 このクエリは、xs: string として型指定された単純型の値のシーケンスを返します。  
  
```  
declare @x xml  
set @x = '<e>1</e><e>2</e>'  
select @x.query('/e[1] cast as xs:string?')  
go  
```  
  
### <a name="example-b"></a>例 B  
 次の例では、型指定された xml 変数をクエリします。 この例では、まず XML スキーマ コレクションを作成しています。 次に、XML スキーマコレクションを使用して、型指定された xml 変数を作成します。 スキーマでは、変数に割り当てられている XML インスタンスの入力情報が提供されます。 その後、変数に対してクエリを指定しています。  
  
```  
create xml schema collection myCollection as N'  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">  
      <xs:element name="root">  
            <xs:complexType>  
                  <xs:sequence>  
                        <xs:element name="A" type="xs:string"/>  
                        <xs:element name="B" type="xs:string"/>  
                        <xs:element name="C" type="xs:string"/>  
                  </xs:sequence>  
            </xs:complexType>  
      </xs:element>  
</xs:schema>'  
go  
```  
  
 次のクエリでは、ドキュメントインスタンス内の最上位レベルの <> 要素の数がわからないため、静的なエラーが返され `root` ます。  
  
```  
declare @x xml(myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
          <root><A>4</A><B>5</B><C>6</baz></C>'  
select @x.query('/root/A cast as xs:string?')  
go  
```  
  
 式にシングルトン <> 要素を指定すると、 `root` クエリは成功します。 このクエリは、xs: string として型指定された単純型の値のシーケンスを返します。  
  
```  
declare @x xml(myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
              <root><A>4</A><B>5</B><C>6</C></root>'  
select @x.query('/root[1]/A cast as xs:string?')  
go  
```  
  
 次の例では、xml 型の変数に、XML スキーマコレクションを指定する document キーワードが含まれています。 これは、XML インスタンスが1つのトップレベル要素を持つドキュメントである必要があることを示します。 XML インスタンスに2つの <> 要素を作成すると `root` 、エラーが返されます。  
  
```  
declare @x xml(document myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
              <root><A>4</A><B>5</B><C>6</C></root>'  
go  
```  
  
 最上位の要素を1つだけ含めるようにインスタンスを変更すると、クエリが機能します。 ここでも、クエリは、xs: string として型指定された単純型の値のシーケンスを返します。  
  
```  
declare @x xml(document myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>'  
select @x.query('/root/A cast as xs:string?')  
go  
```  
  
## <a name="implicit-casting"></a>暗黙のキャスト  
 暗黙のキャストを使用できるのは、数値型と型指定されていないアトミック型だけです。 たとえば、次の **min ()** 関数は、2つの値の最小値を返します。  
  
```  
min(xs:integer("1"), xs:double("1.1"))  
```  
  
 この例では、XQuery の **min ()** 関数に渡される2つの値の型が異なります。 したがって、 **整数** 型が **double** に上位変換され、2つの **double** 値が比較される場合、暗黙的な変換が実行されます。  
  
 この例のような型の上位変換は、次の規則に従って行われます。  
  
-   組み込みの派生数値型は、その基本型に昇格させることができます。 たとえば、 **integer** を **decimal** に昇格させることができます。  
  
-   **Decimal** は **float** に上位変換され、 **float** は **double** に上位変換される場合があります。  
  
 暗黙のキャストを使用できるのは数値型だけなので、次のキャストは許可されません。  
  
-   文字列型間の暗黙のキャストは許可されません。 たとえば、2つの **文字列** 型が想定されている場合に、 **文字列** と **トークン** を渡すと、暗黙的なキャストは発生せず、エラーが返されます。  
  
-   数値型から文字列型への暗黙的なキャストは許可されていません。 たとえば、文字列型のパラメーターが必要な関数に整数型の値を渡すと、暗黙のキャストは行われず、エラーが返されます。  
  
## <a name="casting-values"></a>値のキャスト  
 ある型から別の型へキャストすると、実際の値は元の型の値空間からキャスト先の型の値空間に変換されます。 たとえば、xs:decimal から xs:double にキャストすると、decimal 値が double 値に変換されます。  
  
 次に、いくつかの変換の規則を示します。  
  
##### <a name="casting-a-value-from-a-string-or-untypedatomic-type"></a>String 型または untypedAtomic 型からの値のキャスト  
 string または untypedAtomic 型にキャストされる値は、キャスト先の型の規則に基づいて値が評価されるのと同じ方法で変換されます。 これには、最終的なパターンと空白の処理規則が含まれます。 たとえば、次のキャストは成功し、double 値 1.1e0 が生成されます。  
  
 `xs:double("1.1")`  
  
 文字列型または untypedAtomic 型から xs: base64Binary や xs: hexBinary などのバイナリ型にキャストする場合、入力値はそれぞれ base64 または16進エンコードである必要があります。  
  
##### <a name="casting-a-value-to-a-string-or-untypedatomic-type"></a>文字列型または untypedAtomic 型への値のキャスト  
 String 型または untypedAtomic 型にキャストすると、値は XQuery 正規構文表現に変換されます。 これは、入力時に特定のパターンや他の制約に従っていた値が、制約どおりに表記されない可能性があることを意味します。  これについてユーザーに通知するために、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 型の制約がスキーマコレクションに読み込まれたときに警告を提供することによって、型の制約が問題になる可能性のあるフラグ型です。  
  
 xs:float 型、xs:double 型、またはこれらのサブタイプの値を string 型または untypedAtomic 型にキャストする場合、値は科学的表記法で表現されます。 これは、値の絶対値が 1.0E-6 未満であるか、1.0E6 以上である場合にのみ行われます。 つまり、0 は科学的表記法で 0.0E0 にシリアル化されます。  
  
 たとえば、 `xs:string(1.11e1)` は文字列値を返し、 `"11.1"` `xs:string(-0.00000000002e0)` は文字列値を返し `"-2.0E-11"` ます。  
  
 xs:base64Binary や xs:hexBinary などバイナリ型から string 型または untypedAtomic 型にキャストする場合、バイナリ値はそれぞれ base64 または hex エンコード形式で表現されます。  
  
##### <a name="casting-a-value-to-a-numeric-type"></a>数値型への値のキャスト  
 ある数値型の値を別の数値型の値にキャストすると、文字列のシリアル化を行わずに値が1つの値空間から別の値にマップされます。 値が対象の型の制約を満たしていない場合は、次の規則が適用されます。  
  
-   ソース値が既に数値で、対象の型が xs: float または-INF または INF 値を許可するサブタイプである場合、値が正の値または-INF (値が負の場合) の場合、値は INF にマップされます。 対象の型で INF または-INF が許可されておらず、オーバーフローが発生した場合、キャストは失敗し、このリリースの SQL Server の結果は空のシーケンスになります。  
  
-   元の値が既に数値型で、キャスト先の型が 0、-0e0、または 0e0 を許容する数値型の場合に、元の数値がキャスト後オーバーフローするようなときは、値が次のようにマップされます。  
  
    -   キャスト先の型が decimal の場合、値は 0 にマップされます。  
  
    -   値が負のアンダーフローになる場合、値は -0e0 にマップされます。  
  
    -   値が float 型または double 型の正のアンダーフローの場合、値は0e0 にマップされます。  
  
     対象の型の値空間にゼロが含まれていない場合、キャストは失敗し、結果は空のシーケンスになります。  
  
     値を xs:float、xs:double、またはそのサブタイプなどのバイナリ浮動小数点型にキャストすると、有効桁数が失われる可能性があることに注意してください。  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 制限事項は次のとおりです。  
  
-   浮動小数点値 NaN はサポートされていません。  
  
-   Castable 値は、ターゲット型の実装制限によって制限されます。 たとえば、負の年の日付文字列を **xs: date** にキャストすることはできません。 実行時に値が指定された場合、このようなキャストでは、(実行時エラーになるのではなく) 空のシーケンスが返されます。  
  
## <a name="see-also"></a>参照  
 [XML データのシリアル化の定義](../relational-databases/xml/define-the-serialization-of-xml-data.md)  
  
  
